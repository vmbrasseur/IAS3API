## Identifiers

Each item at Internet Archive has a identifier. An identifier is composed of any unique combination of alphanumeric characters, underscore ( _ ) and dash ( - ). While there are no official limits it is strongly suggested that identifiers be between 5 and 80 characters in length.

Identifiers must be unique across the entirety of Internet Archive, not simply unique within a single collection.

Once defined an identifier **can not** be changed. It will travel with the item or object and is involved in every manner of accessing or referring to the item.

In IAS3, identifiers are defined implicitly in the target URL. For example:

    curl --location --header 'x-amz-auto-make-bucket:1' \
    --header "Authorization: LOW $accesskey:$secret" \
    --header "x-archive-meta-collection:test_collection" \
    --upload-file /Users/archive/Desktop/The_Open_Source_Way_03.pdf \
    http://s3.us.archive.org/vmb_tosw_trial_upload_03/The_Open_Source_Way_03.pdf

The identifier in this command is `vmb_tosw_trial_upload_03`. The item may be viewed at its _details_ page. The details page for any item is simply `http://archive.org/details/` followed by the identifier. The details page for this example is:

    http://archive.org/details/vmb_tosw_trial_upload_03
    
Navigation

* [< Passing Authorization Credentials to IAS3](https://github.com/vmbrasseur/IAS3API/blob/master/authcredentials.md)
* [Table of Contents](https://github.com/vmbrasseur/IAS3API)
* [> Anatomy of an IAS3 Request](https://github.com/vmbrasseur/IAS3API/blob/master/requestanatomy.md)

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

