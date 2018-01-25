## Headers

Headers are directives passed to IAS3. They control and define such things as item creation and [metadata](./metadata.md) fields and values.

There are two types of headers:

1. Amazon S3 Headers
1. Internet Archive-specific Headers

### Amazon S3 Headers

While pretty much any [Amazon S3 header](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTCommonRequestHeaders.html) can be used with IAS3, in practice the most common non-authorization header used is:

    x-amz-auto-make-bucket

This header directs IAS3 to create an item record. If this header is used with an upload command, IAS3 will both create an item and upload file(s) to it with a single command.

To enable this behavior, pass the `x-archive-auto-make-bucket` header with a value of `1`. If you do not specify this value you **must** create an item before you attempt to upload to it. 

The default value for this header (if it is not otherwise defined) is `0`. 

This header is only valid in IAS3 `PUT` commands.

### Internet Archive-specific Headers

Internet Archive has implemented specialized headers for controlling certain operations upon objects and files via IAS3.

#### x-archive-cascade-delete

Normal DELETE operation is to remove only the specified file. The `x-archive-cascade-delete` header allows you to delete not only a file but also all derivative and original files associated with it. The [Internet Archive derivatives help page](http://www.archive.org/help/derivatives.php) provides additional information about the files which may be deleted in this operation.

To enable this option, pass the `x-archive-cascade-delete` header with a value of `1`. 

The default value for this header is `0`.

This header only works when DELETING a file within an item. 

**Nota bene:** DELETE is not allowed for items (buckets) in IAS3. You may only DELETE a file and its derivatives.

#### x-archive-ignore-preexisting-bucket

A normal PUT operation including `x-archive-meta-*` headers will overwrite an existing `IDENTIFIER_meta.xml` file. The `x-archive-ignore-preexisting-bucket` header will instead overwrite the existing `IDENTIFIER_meta.xml` file with the `x-archive-meta-*-` header values passed in the same PUT command.

To enable this option, pass the `x-archive-ignore-preexisting-bucket` header with a value of `1`. 

The default value for this header is `0`.

This header only works when PUTting to IAS3.

#### x-archive-keep-old-version

Normal PUT operation will overwrite a file when it is used to upload a file of the same name. A normal DELETE operation will remove the specified file. The `x-archive-keep-old-version` header will rename the specified file, prepending the filename with `.~~` before proceeding with the PUT or DELETE operation.

To enable this option, pass the `x-archive-keep-old-version` header with a value of `1`. 

The default value for this header is `0`.

This header works for both PUT and DELETE for IAS3.

**Caution!** This header is experimental. Its use could result in unexpected results if interleaved with PUTs which do not use this header.

#### x-archive-meta-

The `x-archive-meta-*` header is used for setting metadata values for an item. This header is discussed in detail in the [Metadata](./metadata.md) section of this document.

#### x-archive-queue-derive

Normal operation after a file has been PUT into an item is to queue it for [derivation to other file formats](http://www.archive.org/help/derivatives.php). PUTting either a very large file or a large number of files can bog down the derivation process and slow system performance. In these instances it is preferable to disable automatically derive queueing.

Please note: Files may be queued for derivation following upload. To queue an individual file, navigate to the item detail page on Internet Archive and click the _Edit Item!_ link at the top. If you have several files which need to be queued, [contact Internet Archive](mailto:info@archive.org?subject=[Queue for Derive]) for assistance.

To disable automated creation of derivative files, pass the `x-archive-queue-derive` header with a value of `0`. 

The default value for this header is `1`.

This header works only when PUTting to IAS3.

#### x-archive-size-hint

If the total size of files in your item will exceed 10 gigabytes, Internet Archive recommends you declare the size at the time of bucket creation. This allows the Internet Archive catalog to more easily place the item for storage, facilitating a potential speed boost to the upload.

To enable this option, pass the `x-archive-size-hint` header with a value of the file size **in bytes**.

If this header is not defined IAS3 will attempt to default to the value in the `content-length` header.

This header works only when PUTting to IAS3.

Navigation

* [< Anatomy of an IAS3 Request](https://github.com/vmbrasseur/IAS3API/blob/master/requestanatomy.md)
* [Table of Contents](https://github.com/vmbrasseur/IAS3API)
* [> Metadata](https://github.com/vmbrasseur/IAS3API/blob/master/metadata.md)

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

