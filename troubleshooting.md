## Troubleshooting and FAQs

### Viewing a log of your IAS3 object

Each file uploaded to Internet Archive via IAS3 will have a log file. To view the log, append `?log` to the URL of the endpoint. For example:

    http://s3.us.archive.org/sam-s3-test-08/demo-intro-to-k.pdf?log

**Please note:** The log format may change at any time.

### My file isn't appearing in the item!

When a file is added to an item it is staged in temporary storage and ingested via the Archive's content management system. While this usually happens very quickly, during periods of heavy system load this process can take a few minutes.

It is also possible that you are viewing a cached version of the item's detail page. Please either clear your web browser's cache or append this parameter to the item's URL:

    reCache=1

### Is there sandbox I can use for testing IAS3?

Internet Archive provides a collection where you can test your item creation and uploads. Items assigned to this collection are removed from the Archive once every thirty days or so. To use this collection, assign your test items to it using this header:

    x-archive-meta-collection:test_collection

Please remember that [item identifiers](./identifiers.md) must be unique across the entire Archive, including for items in the test collection. Your test scripts may need to be modified to avoid identifier collision once you start creating and uploading to non-test items. (read: use throwaway test identifier names for throwaway test items)

### What happens to my item/file after uploading?

Several processes will operate on your item after it has been created and after each file is added to it. These processes include archiving the content, deriving new files from your originals and backing up the item and its contents. You may view the progress of any of these processes on the item's _catalog_ page:

    http://www.archive.org/catalog.php?history=1&identifier=IDENTIFIER

Clicking the `task_id` for a process will display a detailed log for it.

You may also reach this page by clicking the 'Item History' link on the item's detail page on Internet Archive.

### Is there any way to control how files derive?

You may use either the [`IDENTIFIER_rules.conf`](./specialfiles.md) file or the [`x-archive-queue-derive`](./headers.md) header to control the creation of [derivative files](http://www.archive.org/help/derivatives.php) from your originals.

Navigation

* [< A note on downloading](https://github.com/vmbrasseur/IAS3API/blob/master/downloading.md)
* [Table of Contents](https://github.com/vmbrasseur/IAS3API)
* [> Code Examples](https://github.com/vmbrasseur/IAS3API/blob/master/examples/README.md)

-----

_Like the API? Like [Internet Archive](http://archive.org)? Please consider supporting them with a [donation](http://archive.org/donate/)!_

