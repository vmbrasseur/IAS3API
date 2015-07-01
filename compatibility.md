## Compatibiity with Amazon S3

Internet Archive strives to make IAS3 compatible with current Amazon S3 client code. Ideally running the following command–replacing `amazonaws.com` with `us.archive.org`–on your S3 client code would allow you to use IAS3 with no further changes necessary:

    perl -pi -e  's/amazonaws.com/us.archive.org/g' *

Some Amazon S3 clients obey configuration files, many of will will allow you to define the preferred S3 hostname. Setting this hostname to `s3.us.archive.org` in the configuration file should allow the client code to upload to Internet Archive with no further changes.

For instance, adding the following to your `~/.s3cfg` configuration file for [s3cmd](http://s3tools.org/s3cmd), a popular Amazon S3 client, will allow you to connect to IAS3:

    [default]
		access_key = YOUR-ACCESS-KEY	
		secret_key = YOUR-SECRET-KEY
		host_base = s3.us.archive.org
		host_bucket = %(bucket)s.s3.us.archive.org

The `access_key` and `secret_key` are available on [your Internet Archive patron record](http://www.archive.org/account/s3.php).

Navigation

* [< System Requirements](https://github.com/vmbrasseur/IAS3API/blob/master/systemrequirements.md)
* [Table of Contents](https://github.com/vmbrasseur/IAS3API)
* [> Passing Authorization Credentials to IAS3](https://github.com/vmbrasseur/IAS3API/blob/master/authcredentials.md)

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

