## Extract from a script for uploading multiple files to an item using LWP

This is a portion of a Perl script. It shows how one could use [LWP](https://metacpan.org/pod/LWP) to upload multiple files to a single item record.

_NOTA BENE:_ This is only a partial script and will not work as-is.
    
    my $ua = LWP::UserAgent->new();
    $ua->agent('upload_via_IAS3/' . VERSION);
    $ua->timeout(20);
    $ua->env_proxy;
    
    $ua->default_headers->push_header('authorization'=>"LOW $ias3keys");
    
    # start actual upload tasks, doing some optimization.
    # - items with no file to upload are not created
    # - item creation is always combined with the first file upload
    my @uploadQueue = @{$task->{files}};

    while (@uploadQueue) {
        my $file = shift @uploadQueue;
        my $uripath = "/" . $file->{item}{name} . "/" . $file->{filename};

        warn "File: ", $file->{file}, " -> ", $uripath, "\n";

        if (!$forceupload && $file->{uploaded}) {
            my $last = $file->{uploaded};

            # this file was uploaded in previous run. re-upload it only when
            # something has changed.
            if ($file->{mtime} &lt;= $last->{mtime} &&
                $file->{item}{name} eq $last->{itemName} &&
                $file->{filename} eq $last->{filename}) {
                    warn "skipping - no change since last upload\n";
                    next;
            }
        }

        if ($checkstore) {
            my $dlurl = IADLURLBASE . $uripath;

            print STDERR "checking ", $dlurl, "...\n" if $verbose;

            my $res = $ua->head($dlurl);

            if ($res->is_success) {
                # file exists - check date (of last upload) against file's mtime
                my $m = $res->headers->{'date'};

                if ($m && str2time($m) >= $file->{mtime}) {
                    warn "skipping - upload date later than file's mtime\n";
                    next;
                }
            } 
            else {
                # 404 or other failure - upload the file
                print $res->status_line, "\n";
            }
        }
      
        my $waitUntil = $file->{waitUntil};

        if (defined $waitUntil) {
            my $sec = $waitUntil - time();

            while ($sec > 0) {
                print STDERR "holding off $sec second", ($sec > 1 ? 's' : ''), "...   ";
                sleep(1);
                $sec--;
            } 

            continue { print STDERR "\r"; }
            print STDERR "\n";
            delete $file->{waitUntil};
        }

        # ok, ready to go
        my $item = $file->{item};
        my @headers = ();

        # prepare item metadata if the item hasn't been created yet (in this
        # session) - it might exist on the server.
        unless ($item->{created}) {
            my $metadata = $item->{metadata};
    
            # prepare actual HTTP headers for metadata
            push(@headers, 'x-amz-auto-make-bucket', 1);
            
            # As metadata (most often 'collection' and 'subject') may have multiple
            # values, %metadata has an array for each metadata name (in come case,
            # notably 'title', may be a scalar). If there in fact multiple values,
            # we use metadata header in indexed form. If there's only one value
            # (either in an array or as a scalar), we use basic form. Special metadata
            # 'collection' is also handled by this same logic.
            while (my ($h, $v) = each %$metadata) {
                push(@headers, metadataHeaders($h, $v));
            }
            
            # add metadata headers for collections item gets associated with
            my @collectionNames = map($_->{name}, @{$item->{collections}});

            push(@headers, metadataHeaders('collection', \@collectionNames));
            
            # overwrite existing bucket unless user explicitly told not to.
            unless ($keepExistingMetadata) {
                push(@headers, 'x-archive-ignore-preexisting-bucket', '1');
            }
            
            # size-hint
            if ($item->{size}) {
                push(@headers, 'x-archive-size-hint', $item->{size});
            }
        } #end of unless


        # no-derive flag should go with all files to help reduce immediate
        # system load. Can queue derives manually later.
        if ($noDerive) {
            push(@headers, 'x-archive-queue-derive', '0');
        }

        # Expect header
        push(@headers, 'expect', '100-continue');
    
        my $uri = IAS3URLBASE . $uripath;
        my $content = $file->{path};
        
        if ($verbose) {
            print STDERR "PUT $uri\n";

            for (my $i = 0; $i &lt; $#headers; $i += 2) {
                print STDERR $headers[$i], ":", $headers[$i + 1], "\n";
            }
        }
    
        if ($dryrun) {
            print STDERR "## dry-run; not making actual request\n";
        } 
        else {
            # use of custom PUT_FILE is for efficient handling of large files.
            # see comment on PUT_FILE above.
            my $req = PUT_FILE $uri, $content, @headers;

            #print STDERR $req->as_string;
            my $res = $ua->request($req);

            print STDERR "\n";

            if ($res->is_success) {
                print $res->status_line, "\n";
                $res->headers->scan(sub { print "$_[0]: $_[1]\n"; }) if $verbose;
                print $res->content, "\n" if $verbose;
                print "\n";
            } 
            else {
                print $res->status_line, "\n", $res->content, "\n\n";
                if ($res->code == 503) {
                    # Service Unavailable - asking to slow down
                    $file->{waitUntil} = time() + 120;
                    # put it at the head so that it blocks transfer
                    unshift(@uploadQueue, $file);
                } 
                elsif (++$file->{failCount} &lt; 5) {
                    $file->{waitUntil} = time() + 120;
                    push(@uploadQueue, $file);
                } 
                else {
                    # give up
                }
               next;
            }
        }
        
        $item->{created} = 1;
    }
