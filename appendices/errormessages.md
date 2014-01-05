## IAS3 Error Messages

IAS3 may return the following error messages:

| Error Code | Error Message | HTTP Code Returned |
| ---------- | ------------- | ------------------ |
| AccessDenied | Access Denied | 403 Forbidden |
| AccountProblem | There is a problem with your AWS account that prevents the operation from completing successfully. Please contact customer service at webservices@amazon.com. | 403 Forbidden |
| AmbiguousGrantByEmailAddress | The e-mail address you provided is associated with more than one account. | 400 Bad Request |
| BadDigest | The Content-MD5 you specified did not match what we received. | 400 Bad Request |
| BucketAlreadyExists | The requested bucket name is not available. The bucket namespace is shared by all users of the system. Please select a different name and try again. | 409 Conflict |
| BucketAlreadyOwnedByYou | Your previous request to create the named bucket succeeded and you already own it. | 409 Conflict |
| BucketNotEmpty | The bucket you tried to delete is not empty. | 409 Conflict |
| CredentialsNotSupported | This request does not support credentials. | 400 Bad Request |
| CrossLocationLoggingProhibited | Cross location logging not allowed. Buckets in one geographic location cannot log information to a bucket in another location. | 403 Forbidden |
| EntityTooSmall | Your proposed upload is smaller than the minimum allowed object size. | 400 Bad Request |
| EntityTooLarge | Your proposed upload exceeds the maximum allowed object size. | 400 Bad Request |
| ExpiredToken | The provided token has expired. | 400 Bad Request |
| IncompleteBody | You did not provide the number of bytes specified by the Content-Length HTTP header | 400 Bad Request |
| IncorrectNumberOfFilesInPostRequest | POST requires exactly one file upload per request. | 400 Bad Request |
| InlineDataTooLarge | Inline data exceeds the maximum allowed size. | 400 Bad Request |
| InternalError | We encountered an internal error. Please try again. | 500 Internal Server Error |
| InvalidAccessKeyId | The AWS Access Key Id you provided does not exist in our records. | 403 Forbidden |
| InvalidAddressingHeader | You must specify the Anonymous role. | N/A |
| InvalidArgument | Invalid Argument | 400 Bad Request |
| InvalidBucketName | The specified bucket is not valid. | 400 Bad Request |
| InvalidDigest | The Content-MD5 you specified was an invalid. | 400 Bad Request |
| InvalidLocationConstraint | The specified location constraint is not valid. | 400 Bad Request |
| InvalidPayer | All access to this object has been disabled. | 403 Forbidden |
| InvalidPolicyDocument | The content of the form does not meet the conditions specified in the policy document. | 400 Bad Request |
| InvalidRange | The requested range cannot be satisfied. | 416 Requested Range Not Satisfiable |
| InvalidSecurity | The provided security credentials are not valid. | 403 Forbidden |
| InvalidSOAPRequest | The SOAP request body is invalid. | 400 Bad Request |
| InvalidStorageClass | The storage class you specified is not valid. | 400 Bad Request |
| InvalidTargetBucketForLogging | The target bucket for logging does not exist, is not owned by you, or does not have the appropriate grants for the log-delivery group.  | 400 Bad Request |
| InvalidToken | The provided token is malformed or otherwise invalid. | 400 Bad Request |
| InvalidURI | Couldn't parse the specified URI. | 400 Bad Request |
| KeyTooLong | Your key is too long. | 400 Bad Request |
| MalformedACLError | The XML you provided was not well-formed or did not validate against our published schema. | 400 Bad Request |
| MalformedPOSTRequest  | The body of your POST request is not well-formed multipart/form-data. | 400 Bad Request |
| MaxMessageLengthExceeded | Your request was too big. | 400 Bad Request |
| MaxPostPreDataLengthExceededError | Your POST request fields preceding the upload file were too large. | 400 Bad Request |
| MetadataTooLarge | Your metadata headers exceed the maximum allowed metadata size. | 400 Bad Request |
| MethodNotAllowed | The specified method is not allowed against this resource. | 405 Method Not Allowed |
| MissingAttachment | A SOAP attachment was expected, but none were found. | N/A |
| MissingContentLength | You must provide the Content-Length HTTP header. | 411 Length Required |
| MissingSecurityElement | The SOAP 1.1 request is missing a security element. | 400 Bad Request |
| MissingSecurityHeader | Your request was missing a required header. | 400 Bad Request |
| NoLoggingStatusForKey | There is no such thing as a logging status sub-resource for a key. | 400 Bad Request |
| NoSuchBucket | The specified bucket does not exist. | 404 Not Found |
| NoSuchKey | The specified key does not exist. | 404 Not Found |
| NotImplemented | A header you provided implies functionality that is not implemented. | 501 Not Implemented |
| NotSignedUp | Your account is not signed up for the Amazon S3 service. You must sign up before you can use Amazon S3. You can sign up at the following URL: http://aws.amazon.com/s3 | 403 Forbidden |
| OperationAborted | A conflicting conditional operation is currently in progress against this resource. Please try again. | 409 Conflict |
| PermanentRedirect | The bucket you are attempting to access must be addressed using the specified endpoint. Please send all future requests to this endpoint. | 301 Moved Permanently |
| PreconditionFailed | At least one of the pre-conditions you specified did not hold. | 412 Precondition Failed |
| Redirect | Temporary redirect. | 307 Moved Temporarily |
| RequestIsNotMultiPartContent | Bucket POST must be of the enclosure-type multipart/form-data. | 400 Bad Request |
| RequestTimeout | Your socket connection to the server was not read from or written to within the timeout period. | 400 Bad Request |
| RequestTimeTooSkewed | The difference between the request time and the server's time is too large. | 403 Forbidden |
| RequestTorrentOfBucketError | Requesting the torrent file of a bucket is not permitted. | 400 Bad Request |
| SignatureDoesNotMatch | The request signature we calculated does not match the signature you provided. Check your AWS Secret Access Key and signing method. For more information, see Authenticating REST Requests and Authenticating SOAP Requests for details. | 403 Forbidden |
| SlowDown | Please reduce your request rate. | 503 Service Unavailable |
| TemporaryRedirect | You are being redirected to the bucket while DNS updates. | 307 Moved Temporarily |
| TokenRefreshRequired | The provided token must be refreshed. | 400 Bad Request |
| TooManyBuckets | You have attempted to create more buckets than allowed. | 400 Bad Request |
| UnexpectedContent | This request does not support content. | 400 Bad Request |
| UnresolvableGrantByEmailAddress | The e-mail address you provided does not match any account on record. | 400 Bad Request |
| UserKeyMustBeSpecified | The bucket POST must contain the specified field name. If it is specified, please check the order of the fields. | 400 Bad Request |

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

