## Setting Metadata Values via Files

While the preferred and recommended method for setting Internet Archive item metadata is via headers, it is possible to provide files containing metadata. If you choose to provide a metadata file instead of using headers it is strongly recommended that the metadata file be the first uploaded during item creation.

When providing a metadata file, please provide only one file per item. It is not necessary to provide a metadata file in each format. Additional files will be generated automatically from the one which you provide.

### IDENTIFIER_marc.xml

This file must contain metadata in well-formed [MARCXML](http://www.loc.gov/standards/marcxml/) format. 

It must be named appropriately or it will not be recognized. The proper naming scheme is the items [identifier](./identifiers.md) followed by `_marc.xml`.

An [example IDENTIFIER_marc.xml file](./appendices/identifier_marc_xml.md) can be found in the Appendix.

### IDENTIFIER_meta.mrc

This file must contain metadata in binary MARC format according to the [ISO 2709](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=41319) standard. 
It must be named appropriately or it will not be recognized. The proper naming scheme is the items [identifier](./identifiers.md) followed by `_marc.xml`.

An [example IDENTIFIER_meta.mrc file](./appendices/identifier_meta_mrc.md) can be found in the Appendix.

### How these metadata files are processed

If an `IDENTIFIER_meta.mrc` file is located it is used to generate an `IDENTIFIER_marc.xml` file. Any existing `IDENTIFIER_marc.xml` file will be overwritten by this operation.

The `IDENTIFIER_marc.xml` file is used to generate a `IDENTIFIER_dc.xml` file of [Dublin Core metadata](http://dublincore.org/). Any existing `IDENTIFIER_dc.xml` file will be overwritten by this operation. The Dublin Core fields are extracted and populated according to the [Library of Congress MARC21 to Dublin Core XSL stylesheet](http://www.loc.gov/standards/marcxml/xslt/MARC21slim2OAIDC.xsl). In addition, Internet Archive will extract information from the following MARCXML fields:

* `041` subfield `a` and `130` subfield `1` are searched for language codes. If multiple language codes are located they are all added to the item's metadata.
* `260` subfield `c` is searched for an item date.
* `010` subfield `a` is searched for the LCCN.

The item's definitive metadata file, `IDENTIFIER_meta.xml` is generated from the `IDENTIFIER_dc.xml` Dublin Core file.

Navigation

* [< Metadata](https://github.com/vmbrasseur/IAS3API/blob/master/metadata.md)
* [Table of Contents](https://github.com/vmbrasseur/IAS3API)
* [> Special Files](https://github.com/vmbrasseur/IAS3API/blob/master/specialfiles.md)

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

