zipinfo
===

List detailed information about a zip archive

## Description

The **zipinfo** command is used to list information about a zip archive. Executing the zipinfo command provides detailed information about zip compressed files.

### Syntax

```shell
zipinfo [options] [parameters]
```

### Options

```shell
-1: List filenames only, one per line;
-2: Similar to -1, but can be used with -h, -t, and -z options;
-h: List archive header only (the archive name);
-l: Similar to -m, but lists the original file size instead of each file's compression ratio;
-m: Similar to -s, but also lists each file's compression ratio;
-M: Pipe output through an internal pager similar to more;
-s: List zip archive contents in a format similar to ls -l;
-t: List total number of files in the archive, the total size (uncompressed and compressed), and the total compression ratio;
-T: List the date and time of each file in the archive in the format YYYYMMDD.HHMMSS;
-v: Verbose mode, displaying detailed information for every file in the archive;
-x <pattern>: Exclude files matching the specified pattern;
-z: Display the archive comment if one exists.
```

### Parameters

File: Specifies the zip archive.
