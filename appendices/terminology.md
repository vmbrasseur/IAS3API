## Terminology

### Bucket

'Bucket' is the Amazon S3 term for a container for your files. For the IAS3 API, a bucket is equivalent to an Internet Archive 'item' (see below).
		
### Collection

A collection is a specialized Internet Archive item used for aggregating related collections and items. An item or collection is assigned to a collection via the [x-archive-meta-collection](../metadata.md) metadata header.

Currently collections can only be created by Internet Archive staff members. Please [contact Internet Archive](mailto:info@archive.org?subject=[Collection Creation Request]) if you need a collection created.

### Derivative

A derivative is a file which Internet Archive will automatically generate from the original file which you provide. Derivatives enable as many people as possible to access the file while also protecting against file format obsolescence. 

Please refer to [the derivatives chart](http://www.archive.org/help/derivatives.php) to see which derivative formats Internet Archive will produce.

### Identifier

Each item at Internet Archive has a identifier. An identifier is composed of any unique combination of alphanumeric characters, underscore ( _ ) and dash ( - ). While there are no official limits it is strongly suggested that they be between 5 and 80 characters in length. 

An identifier must be unique across the entirety of Internet Archive.

### Item

An item is the primary entity of the Internet Archive. All of the files you upload will be contained in items. Each item has its own Internet Archive page, also known as its _details_ page. The details page can be accessed using the following URL pattern:

    http://archive.org/details/IDENTIFIER
