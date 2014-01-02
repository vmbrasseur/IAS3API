## Upload a file to an existing item

This [curl](http://curl.haxx.se/) command can be run at the command line. It will do the following things:

1. Upload the file 'demo-intro-to-k.pdf' to the existing item 'sam-s3-text-08'

    curl --location \<br />
        --header "authorization: LOW $accesskey:$secret" \
        --upload-file /home/samuel/public_html/intro-to-k.pdf \
    http://s3.us.archive.org/sam-s3-test-08/demo-intro-to-k.pdf

