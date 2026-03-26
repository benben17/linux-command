mktemp
===

Create a temporary file or directory

## Description

The **mktemp command** is used to create a temporary file or directory, typically for use within shell scripts to ensure unique and secure naming.

### Syntax

```shell
mktemp [OPTION]... [TEMPLATE]
```

### Options

```shell
-q：Quiet execution; suppress error messages.
-u：Dry run; the temporary file name is generated but the file is not created.
-d：Create a directory instead of a file.
--tmpdir[=DIR]：Interpret TEMPLATE relative to DIR. If DIR is not specified, use $TMPDIR if set, else /tmp.
```

### Parameters

Template: A template for the filename, which must include at least three 'X's in the last component (e.g., `tmp.XXXXXX`). If omitted, the default is `tmp.XXXXXXXXXX`.
