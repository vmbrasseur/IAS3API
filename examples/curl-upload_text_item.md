## Upload a PDF document to a new text-typed item.

This [curl](http://curl.haxx.se/) command can be run at the command line. It will do the following things:

1. Create a new item (aka bucket) on Internet Archive with the identifier `sam-s3-text-08`
1. Assign the item to the 'text' mediatype, meaning it will be displayed with an online ebook reader
1. Upload the file `demo-intro-to-k.pdf` to the item

-----

    curl --location --header 'x-amz-auto-make-bucket:1' \
        --header 'x-archive-meta01-collection:opensource' \
        --header 'x-archive-meta-mediatype:texts' \
        --header 'x-archive-meta-sponsor:Andrew W. Mellon Foundation' \
        --header 'x-archive-meta-language:eng' \
        --header "authorization: LOW $accesskey:$secret" \
        --upload-file /home/samuel/public_html/intro-to-k.pdf \
    http://s3.us.archive.org/sam-s3-test-08/demo-intro-to-k.pdf
