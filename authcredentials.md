## Passing Authorization Credentials to IAS3

[Authorization credentials](http://www.archive.org/account/s3.php) may be passed to IAS3 by your Amazon S3-compatible client via configuration file (see example in the [Compatibility](./compatibility.md) section of this documentation). 

In addition there is a clear text password mode. To use this mode, pass your access and secret keys as values to the `Authorization` header:

    Authorization: LOW $accesskey:$secret

This is the authorization method shown in most of the examples in this document but it is **not** recommended for production code. Clear text passwords are an immense security risk.

Navigation

* [< Compatibility with Amazon S3](https://github.com/vmbrasseur/IAS3API/blob/master/compatibility.md)
* [Table of Contents](https://github.com/vmbrasseur/IAS3API)
* [> Identifiers](https://github.com/vmbrasseur/IAS3API/blob/master/identifiers.md)

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

