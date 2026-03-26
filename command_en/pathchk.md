pathchk
===

Checks whether file names are valid or portable.

## Description

The **pathchk command** is used to check whether one or more file names are valid (i.e., can be created on the current system) or portable to other POSIX systems.

### Syntax

```shell
pathchk [options] [file...]
```

### Options

```shell
-p: Check for portability to most POSIX systems.
-P: Check for empty names and names starting with "-".
--portability: Check for portability to all POSIX systems (equivalent to -p -P).
--help: Display help information.
--version: Display version information.
```

### Parameters

*   File: The file path(s) to check.
