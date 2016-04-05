## Destroy then update the metadata for an existing item

This [curl](http://curl.haxx.se/) command can be run at the command line. It will do the following things:

1. Destroy all existing metadata for the item with the ID 'sam-s3-text-08'
1. Set values for the title, collection, and mediatype metadata fields

-----

    curl --location \
        --header 'x-archive-ignore-preexisting-bucket:1' \
        --header 'x-archive-meta01-collection:opensource' \
        --header 'x-archive-meta-mediatype:texts' \
        --header 'x-archive-meta-title:Fancy new title' \
        --header "authorization: LOW $accesskey:$secret" \
        --header 'Content-Length:0' \
        --request PUT \
    http://s3.us.archive.org/sam-s3-test-08
