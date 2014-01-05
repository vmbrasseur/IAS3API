## Requirements (system and otherwise)

In order to use IAS3, you must have:

* An internet connection
* An Internet Archive [patron account](http://www.archive.org/account/login.createaccount.php)
* [API keys](http://www.archive.org/account/s3.php) for IAS3
* Client code which supports the Amazon S3 API. Most examples in this document use [curl](http://curl.haxx.se/) for simplicity. If you choose to use curl or libcurl to interface with IAS3 please be sure you are using version 7.19 or higher. These versions have excellent `HTTP 100 Continue` support.
