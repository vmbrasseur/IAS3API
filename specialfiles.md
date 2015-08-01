## Special Files in the Item

Each Internet Archive item is comprised of several files. Many of these files are automatically generated and **should not** be either removed or modified.

### IDENTIFIER_meta.xml

`IDENTIFIER_meta.xml` is the definitive metadata file for the item. It is automatically generated at item creation time using the metadata provided either [via headers](./metadata.md) or [via files](./metadatafiles.md).

Please **do not** delete or modify this file. If you must modify the item's metadata, please either use the "Edit Item!" link at the top of its detail page or submit updated metadata via the IAS3 API. See the [x-archive-ignore-preexisting-bucket](./headers.md) header for additional information about updating an item's metadata via IAS3.

### IDENTIFER_dc.xml

The item metadata in [Dublin Core format](http://dublincore.org/).

Please **do not** delete or modify this file. If you must modify the item's metadata, please either use the "Edit Item!" link at the top of its detail page or submit updated metadata via the IAS3 API. See the [x-archive-ignore-preexisting-bucket](./headers.md) header for additional information about updating an item's metadata via IAS3.


### IDENTIFIER_files.xml

`IDENTIFIER_files.xml` is an auto-generated file cataloging all of the files contained in the item. In addition to the filenames the `IDENTIFIER_files.xml` file will also list the file format and various hashes for each file. If the file is a [derivative](http://www.archive.org/help/derivatives.php) `IDENTIFIER_files.xml` will list the original file from which it was derived.

For example, here is an extract from the `japanesefairytal00ozak_files.xml` file for [Japanese Fairy Tales](http://www.archive.org/details/japanesefairytal00ozak):

    <file name="japanesefairytal00ozak.epub" source="derivative">
        <format>EPUB</format>
        <original>japanesefairytal00ozak_abbyy.gz</original>
        <mtime>1294020233</mtime>
        <size>1230045</size>
        <md5>1d87b3e04ca0b617e041bbcb0cd7f1a5</md5>
        <crc32>7326f3ce</crc32>
        <sha1>5434df04b1b811b03e7d9a32bde3119d3ca924c8</sha1>
    </file>

Please **do not** delete or modify this file.

### IDENTIFIER_rules.conf

Whereas the [x-archive-queue-derive](./headers.md) header enables or disables queuing files for [deriving](http://www.archive.org/help/derivatives.php) for the entire item, it it possible to disable the creation of certain derive files using the `IDENTIFIER_rules.conf` file. There are three options for selecting which derivative formats to disable via `IDENTIFIER_rules.conf`:

#### Specific File Formats

You may disable creation of specific derivative formats by listing them–one format per line–in the `IDENTIFIER_rules.conf` file. The valid values for file formats can be found in the header rows of the [derivatives chart](http://www.archive.org/help/derivatives.php).

For example, to disable creation of h.264 and Ogg Video derivative files, your `IDENTIFIER_rules.conf` file should contain the following:

    h.264
    Ogg Video

#### Only 'lossy' File Formats

Some derivative file formats (mp3, ogg, ogv, mp4, webm) are considered "lossy" because they use a compression algorithm which produces a file which is not identical to the original. To prevent the creation of lossy derivatives, upload a `IDENTIFIER_rules.conf` file containing this line:

    CAT.lossy

#### All Derivatives

It is possible to disable creation of all derivative files using the `IDENTIFIER_rules.conf` file. This is equivalent to setting the [x-archive-queue-derive](./headers.md) header to a value of 0.

To disable all derivatives, upload a `IDENTIFIER_rules.conf` file containing this line:

    CAT.all

A new or modified `IDENTIFIER_rules.conf` file will not be recognized until a new derive process is initiate for the item. It is currently not possible to initiate this process via the IAS3 API. To initiate the derive process in the Internet Archive interface:

 1. Login to Internet Archive
 1. Navigate to the item's page on Internet Archive
 1. Find the "Edit Item!" link in the upper right of the item
 1. Click the "change the information" link
 1. Click the "Item Manager" link near the top of the page
 1. Click the "derive" button

If now-excluded formats had previously been derived, initiating a derive process will remove the files from the item.

Navigation

* [< Setting Metadata Values via Files](https://github.com/vmbrasseur/IAS3API/blob/master/metadatafiles.md)
* [Table of Contents](https://github.com/vmbrasseur/IAS3API)
* [> A note on downloading](https://github.com/vmbrasseur/IAS3API/blob/master/downloading.md)

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

