## Setting Metadata Values via Headers

[Metadata](http://en.wikipedia.org/wiki/Metadata) is data about data. In the case of Internet Archive items, the metadata describes the contents of the items. Metadata can include information such as the performance date for a concert, the name of the artist, and a set list for the event.

Metadata is a very important element of items in Internet Archive. Metadata allows people to locate and view information. Items with little or poor metadata may never be seen and can become lost.

### The x-archive-meta- Header

The `x-archive-meta-*` header is used to set metadata values for items. 

At this time Internet Archive does not support file-level metadata. Metadata may only be defined at an item level.

All metadata fields are defined as key-value pairs passed via headers. The header format is:

    x-archive-meta-FIELDNAME:FIELDVALUE

For instance, if you are using curl you may set a value for the title metadata field using this header:

    --header "x-archive-meta-title:John Muir on Hetch Hetchy"

Alternatively, you may use the Amazon S3 standard `x-amz-meta-FIELDNAME:FIELDVALUE` header for setting metadata.

Metadata headers are sorted prior to processing. This sorting includes the `x-amz-` or `x-archive-` header prefixes, therefore if you use both of these prefixes when setting metadata values the fields set with `x-amz-` will be processed first and may cause unexpected behavior. To avoid potential problems it is advised that you use either the `x-archive-` or the `x-amz-` header prefix when setting metadata, not both.

All metadata header values are interpreted as UTF-8 encoded characters.

### Repeating Metadata Fields

Certain metadata fields such as `collection` and `subject` can be repeated. To repeat a metadata header you must sequentially number each instance of the header in your command:

    x-archive-meta01-$meta_name:$meta_value_a
    x-archive-meta02-$meta_name:$meta_value_b

Note that the numbering goes on the `-meta-` and **not** on the field name.

For example, if an item contains both PDF and mp3 files you may assign it to both the `texts` and `opensource_audio` collections by including the following two lines in a curl command:

    --header 'x-archive-meta01-collection:texts' 
    --header 'x-archive-meta02-collection:opensource_audio'

### Unicode Metadata Values

`x-archive-meta-*` headers are interpreted as having utf-8 character encoding, however some http clients do not allow the full range of utf-8 bytes to appear in http headers.
As a work around, one can encode a utf-8 meta header with uri encoding.
To do this write all the header data like so: `uri($payload_as_uri_encoded_utf8)`

For example, to set the title of an item to include the unicode snowman include the following line in a curl command:

    --header 'x-archive-meta-title:uri(This%20is%20a%20snowman%20%E2%98%83)'

### Standard Internet Archive Metadata Fields

There are several standard metadata fields recognized for Internet Archive items. All metadata fields are optional.

To use these fields, enter the field name after the `meta-` in the `x-archive-meta-` header.

#### addeddate

Contains the date on which the item was added to Internet Archive.

Please use an [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) compatible format for this date. For instance, these are all valid date formats:

* YYYY
* YYYY-MM-DD
* YYYY-MM-DD HH:MM:SS

While it is possible to set the `addeddate` metadata value it is not recommended. This value is typically set by automated processes.

#### adder

The name of the account which added the item to the Internet Archive.

While is is possible to set the `adder` metadata value it is not recommended. This value is typically set by automated processes.

#### collection

A collection is a specialized item used for curation and aggregation of other items. Assigning an item to a collection defines where the item may be located by a user browsing Internet Archive. To assign an item to a collection, pass its identifier as the value for an `x-archive-meta-collection` header. For example, if you are using curl you can assign an item to the _Community Texts_ collection (identifier: _opensource_) with the following header:

    --header 'x-archive-meta-collection:opensource'

A collection **must** exist prior to assigning any items to it. Currently collections can only be created by Internet Archive staff members. Please [contact Internet Archive](mailto:info@archive.org?subject=[Collection Creation Request]) if you need a collection created.

#### contributor

The value of the `contributor` metadata field is information about the entity responsible for making contributions to the content of the item. This is often the library, organization or individual making the item available on Internet Archive.

The value of this metadata field may contain HTML. `<script>` tags and CSS are not allowed.

#### coverage

The extent or scope of the content of the material available in the item. The value of the `coverage` metadata field may include geographic place, temporal period, jurisdiction, etc. For items which contain multi-volume or serial content, place the statement of holdings in this metadata field.

#### creator

An entity primarily responsible for creating the files contained in the item.

#### credits

The participants in the production of the materials contained in the item.

The value of this metadata field may contain HTML. `<script>` tags and CSS are not allowed.

#### date

The publication, production or other similar date of this item. 

Please use an [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) compatible format for this date. For instance, these are all valid date formats:

#### description

A description of the item.

The value of this metadata field may contain HTML. `<script>` tags and CSS are not allowed.

#### language

The primary language of the material available in the item.

While the value of the `language` metadata field can be any value, Internet Archive prefers they be [MARC21 Language Codes](http://www.loc.gov/marc/languages/language_name.html).

#### licenseurl

A URL to the license which covers the works contained in the item.

Internet Archive recommends (but does not require) [Creative Commons](http://creativecommons.org) licensing. Creative Commons provides a [license selector](http://creativecommons.org/choose/?partner=ia&exit_url=http%3A%2F%2Fwww.archive.org%2Fservices%2Flicense-chooser.php%3Flicense_url%3D%5Blicense_url%5D%26license_name%3D%5Blicense_name%5D%26license_image%3D%5Blicense_button%5D%26deed_url%3D%5Bdeed_url%5D&jurisdiction_choose=1) for finding the correct license for your needs.

#### mediatype

The primary type of media contained in the item. While an item can contain files of diverse mediatypes the value in this field defines the appearance and functionality of the item's detail page on Internet Archive. In particular, the mediatype of an item defines what sort of online viewer is available for the files contained in the item.

The mediatype metadata field recognizes a limited set of values:

* `audio`: The majority of audio items should receive this mediatype value. Items for the [Live Music Archive](http://www.archive.org/details/etree) should instead use the `etree` value.
* `collection`: Denotes the item as a collection to which other collections and items can belong. 
* `data`: This is the default value for mediatype. Items with a mediatype of `data` will be available in Internet Archive but you will not be able to browse to them. In addition there will be no online reader/player for the files.
* `etree`: Items which contain files for the [Live Music Archive](http://www.archive.org/details/etree) should have a mediatype value of `etree`. The Live Music Archive has very specific upload requirements. Please consult the [documentation](http://www.archive.org/about/faqs.php#Live_Music_Archive) for the Live Music Archive prior to creating items for it.
* `image`: Items which predominantly consist of image files should receive a mediatype value of `image`. Currently these items will not available for browsing or online viewing in Internet Archive but they will require no additional changes when this mediatype receives additional support in the Archive.
* `movies`: All videos (television, features, shorts, etc.) should receive a mediatype value of `movies`. These items will be displayed with an online video player.
* `software`: Items with a mediatype of `software` are accessible to browse via Internet Archive's [software collection](http://www.archive.org/details/software). There is no online viewer for software but all files are available for download.
* `web`: The `web` mediatype value is reserved for items which contain web archive [WARC](http://www.digitalpreservation.gov/formats/fdd/fdd000236.shtml) files.

If the mediatype value you set is not in the list above it will be saved but ignored by the system. The item will be treated as though it has a mediatype value of `data`.

If a value is not specified for this field it will default to `data`.

#### noindex

All items will have their metadata included in the Internet Archive search engine. To disable indexing in the search engine, include a `noindex` metadata tag. The value of the tag does not matter. Its presence is enough to trigger not including the metadata in the search engine.

If an item's metadata has already been indexed in the search engine, setting `noindex` will remove it from the index.

Items whose metadata is not not included in the search engine index are not considered "public" per se and therefore will not have a value in the `publicdate` metadata field (see below).

#### notes

Contains user-defined information about the item.

The value of this metadata field may contain HTML. `<script>` tags and CSS are not allowed.

#### pick

Each collection page on Internet Archive may include a "Staff Picks" section. This section will highlight a single item in the collection. This item will be selected at random from the items with a `pick` metadata value of `1`. If there are no items with this `pick` metadata value the "Staff Picks" section will not appear on the collection page.

By default all new items have no `pick` metadata value.

#### publicdate

Items which have had their metadata included in the Internet Archive search engine index are considered to be public. The date the metadata is added to the index is the public date for the item.

Please use an [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) compatible format for this date. For instance, these are all valid date formats:

While it is possible to set the `publicdate` metadata value it is not recommended. This value is typically set by automated processes.

#### publisher

The publisher of the material available in the item.

#### rights

A statement of the rights held in and over the files in the item.

The value of this metadata field may contain HTML. `<script>` tags and CSS are not allowed.

#### subject

Keyword(s) or phrase(s) that may be searched for to find your item. Separate each keyword or phrase with a semicolon (";") character. 

It is helpful but **not** necessary for you to use [Library of Congress Subject Headings](http://id.loc.gov/authorities/subjects.html) for the value of this metadata header.

#### title

The title for the item. This appears in the header of the item's detail page on Internet Archive.

If a value is not specified for this field it will default to the identifier for the item.

#### updatedate

The date on which an update was made to the item. This field is repeatable.

Please use an [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) compatible format for this date. For instance, these are all valid date formats:

While it is possible to set the `publicdate` metadata value it is not recommended. This value is typically set by automated processes.

#### updater

The name of the account which updated the item. This field is repeatable.

While it is possible to set the `updater` metadata value it is not recommended. This value is typically set by automated processes.

#### uploader

The name of the account which uploaded the file(s) to the item.

The uploader has ownership over the item and is allowed to maintain it.

While it is possible to set the `uploader` metadata value it is not recommended. This value is typically set by automated processes.

### Custom Metadata Fields

Internet Archive strives to be metadata agnostic, enabling users to define the metadata format which best suits the needs of their material. In addition to the standard metadata fields listed above you may also define as many custom metadata fields as you require. These metadata fields can be defined ad hoc at item creation or metadata editing time and do not have to be defined in advance. For instance, if your organization uses the [PBCORE](http://pbcore.org/index.php) metadata schema you can include the appropriate metadata fields in your Internet Archive item:

    x-archive-meta-pbcoreGenre:Educational
    x-archive-meta-pbcoreCoverage:"Long Beach, CA"
    x-archive-meta-pbcoreCoverageType:Spatial
    etc.

**PLEASE NOTE!** [RFC 822](http://www.faqs.org/rfcs/rfc822.html) disallows the underscore character ( _ ) in HTTP header names. Therefore to use an underscore in the name of a custom metadata field you must replace the underscore ( _ ) with two hyphens ( -- ). These will be translated into an underscore character when the metadata is processed by the server. For example:

    x-archive-meta-isbn--10:080652510X

This example will generate a metadata field named `isbn_10`.

Navigation

* [< Headers](https://github.com/vmbrasseur/IAS3API/blob/master/headers.md)
* [Table of Contents](https://github.com/vmbrasseur/IAS3API)
* [> Setting Metadata Values via Files](https://github.com/vmbrasseur/IAS3API/blob/master/metadatafiles.md)

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

