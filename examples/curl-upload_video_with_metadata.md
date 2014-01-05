## Add metadata to a video item

This [curl](http://curl.haxx.se/) command can be run at the command line. It will do the following things:

1. Create a new item on Internet Archive with the identifier `electricsheep-flock-244`
1. Assign the item to the 'movies' mediatype, meaning it will be displayed with an online video player
1. Assign values to the collection, title, creator, description, data, year, subject, and licence URL metadata fields

    curl --location --header 'x-archive-ignore-preexisting-bucket:1' \
        --header "authorization: LOW $accesskey:$secret" \
        --header 'x-archive-meta-mediatype:movies' \
        --header 'x-archive-meta-collection:opensource_movies' \
        --header 'x-archive-meta-title:electricsheep-flock-244' \
        --header 'x-archive-meta-creator:Scott Draves and the Electric Sheep' \
        --header 'x-archive-meta-description:Archive of flock 244 of the Electric Sheep, see <a href=http://electricsheep.org >http://electricsheep.org</a> and <a href=http://scottdraves.com > http://scottdraves.com</a>' \
        --header 'x-archive-meta-date:2009' \
        --header 'x-archive-meta-year:2009' \
        --header 'x-archive-meta-subject:electricsheep,alife,art,draves,spotworks,evolution,algorithm' \
        --header 'x-archive-meta-licenseurl:http://creativecommons.org/licenses/by-nc/3.0/us/' \
        --upload-file /dev/null \
    http://s3.us.archive.org/electricsheep-flock-244
