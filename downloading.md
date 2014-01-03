## A note on downloading via IAS3

While the IAS3 API supports both `GET` and `HEAD` methods for retrieving files, higher performance can be achieved via the Internet Archive web architecture

Each file in an Internet Archive item can be retrieved via a `/download/` URL:

    http://archive.org/download/IDENTIFIER/FILENAME.EXT

This is the recommended method for programatically downloading files from Internet Archive.
