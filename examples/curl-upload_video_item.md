## Upload a video file to a new video-typed item

This [curl](http://curl.haxx.se/) command can be run at the command line. It will do the following things:

1. Create a new item (aka bucket) on Internet Archive with the identifer 'ben-plays-piano'
1. Assign the item to the 'movies' mediatype, meaning it will be displayed with an online video player
1. Upload the file 'ben-plays-piano.avi' to the item

    curl --location --header 'x-amz-auto-make-bucket:1' \
        --header 'x-archive-meta01-collection:opensource_movies' \
        --header 'x-archive-meta-mediatype:movies' \
        --header 'x-archive-meta-title:Ben plays piano.' \
        --header "authorization: LOW $accesskey:$secret" \
        --upload-file ben-2009-05-09.avi \
    http://s3.us.archive.org/ben-plays-piano/ben-plays-piano.avi
