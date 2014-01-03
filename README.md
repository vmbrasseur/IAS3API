# Internet Archive S3 API: Documentation

This document covers the technical details of using Internet Archive's S3-like server API, aka "IAS3." The intended audience is a technical user, ideally one who is comfortable in the Linux/UNIX command line environment.

This document is a work in progress. Please use it in conjunction with the [official IAS3 documentation](http://archive.org/help/abouts3.txt">http://archive.org/help/abouts3.txt).

Because the initial writing and research for this documentation occurred in 2011, it is possible (likely) there are errors in it. This document is not created or maintained by [Internet Archive](http://archive.org). Please do not contact them for problems with this document. Instead, please [file a Github issue](https://github.com/vmbrasseur/IAS3API/issues).

## Contents

* [Introduction](./introduction.md)
* [Quick Start](./quickstart.md)
* [System Requirements](./systemrequirements.md)
* [Compatibility with Amazon S3](./compatibility.md)
* [Passing Authorization Credentials to IAS3](./authcredentials.md)
* [Identifiers](./identifiers.md)
* [Anatomy of an IAS3 Request](./requestanatomy.md)
* [Headers](./headers.md)
* [Metadata](./metadata.md)
* [Setting Metadata Values via Files](./metadatafiles.md)
* [Special Files](./specialfiles.md)
* [A note on downloading](./downloading.md)
* [Troubleshooting](./troubleshooting.md)
* [Code Examples](./examples/README.md)
* Appendices
    * [Terminology](./appendices/terminology.md)
    * [An intro to Internet Archive item structure](./appendices/itemstructure.md)
    * [IAS3 HTTP Return Codes](./appendices/returncodes.md)
    * [IAS3 Error Messages](./appendices/errormessages.md)
    * [Default metadata values](./appendices/defaultmetadatavalues.md)
    * [Example IDENTIFIER_marc.xml file](./appendices/identifier_marc_xml.md)
    * [Example IDENTIFIER_meta.mrc file](./appendices/identifier_meta_mrc.md)
