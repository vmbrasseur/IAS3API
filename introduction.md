## Introduction
This document covers the technical details of using Internet Archive's S3-like server API, aka "IAS3." The intended audience is a technical user, ideally one who is comfortable in the Linux/UNIX command line environment.

IAS3 is an [API](http://en.wikipedia.org/wiki/Api) based upon [Amazon's](http://aws.amazon.com/) [Simple Storage Service (aka S3)](http://aws.amazon.com/documentation/s3/). Whereas Amazon's S3 API allows you to store items in the Amazon S3 cloud storage service, the IAS3 API allows you to create items on and upload data to [Internet Archive](http://archive.org).

Because of its similarities to Amazon's S3, **please familiarize yourself with the [Amazon S3 documentation](http://docs.amazonwebservices.com/AmazonS3/latest/dev/) before using Internet Archive's IAS3.**

In Internet Archive terminology, an _item_ maps directly onto the Amazon S3 concept of a [bucket](http://docs.aws.amazon.com/general/latest/gr/glos-chap.html#B). IAS3 allows you to create items, populate them with files, and maintain the metadata for the item (Internet Archive currently does not support file-level metadata). You can also use IAS3 to control certain elements of file processing behavior. 

Because Internet Archive items are analogous to Amazon S3 buckets they can be accessed using similar URL addresses. Items are typically accessed on Internet Archive using the IA-specific `details/IDENTIFIER` format. For instance:

    http://www.archive.org/details/Sita_Sings_the_Blues

The link above will present the _details page_ for the item on Internet Archive. This same item is also available in an S3-like format of:

    http://s3.us.archive.org/Sita_Sings_the_Blues

Where `http://s3.us.archive.org` is the base URL used for all IAS3 commands. Both of these URLs will return XML containing information about the item.

Each file contained in an item can similarly be used as an S3-like key in a URL:

    http://Sita_Sings_the_Blues.s3.us.archive.org/Sita_Sings_the_Blues_small.mp4

Performing a `PUT` on the Internet Archive equivalent to an S3 endpoint will result in the creation of a new item in Internet Archive. Files may be added to the item in the same manner. Both of these operations may be combined in a single `PUT` command. For example, using [curl](http://curl.haxx.se/):

    curl --location --header 'x-amz-auto-make-bucket:1' \
    --header 'x-archive-meta01-collection:opensource' \
    --header 'x-archive-meta-mediatype:texts' \
    --header 'x-archive-meta-sponsor:Andrew W. Mellon Foundation' \
    --header 'x-archive-meta-language:eng' \
    --header "authorization: LOW $accesskey:$secret" \
    --upload-file /home/samuel/public_html/intro-to-k.pdf \
    http://s3.us.archive.org/sam-s3-test-08/demo-intro-to-k.pdf

These header fields are explained in more detail in the [Headers](./headers.md) and [Metadata](./metadata.md) sections of this documentation.

### How IAS3 Differs From Amazon S3

IAS3 differs from Amazon's S3 API in several significant ways:

* IAS3 does not allow DELETE for buckets, only for files. Attempting to DELETE a bucket will result in a _Not Authorized_ error.
* IAS3 supports the HTTP 1.1 REST interface for S3 but **not** the SOAP interface.
* IAS3 is much more likely to issue `HTTP 307 Location` redirects than Amazon S3, therefore it is advised that you use an S3-compatible client with good `HTTP 100 Continue` support (for example, curl version 7.19 and higher).
* Amazon S3 allows users to [set ACLs for buckets and objects](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketPUTacl.html). IAS3 does not. Instead, all items are created with [ACLs](http://en.wikipedia.org/wiki/Access_control_list) of world readable and item uploader writable.
* Amazon S3's POST and COPY are not implemented in IAS3.
* IAS3 ignores HTTP 1.1 Range headers.

In addition, IAS3 also supports several of its own headers. These are discussed in more detail in the [Headers](./headers.md) section of this documentation.

Navigation:

* [< Table of Contents](https://github.com/vmbrasseur/IAS3API) 
* [> Summary of API Functionality and FAQs](https://github.com/vmbrasseur/IAS3API/blob/master/summary.md)

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

