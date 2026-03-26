bzcat
===

Decompress files to standard output.

## Description

The **bzcat command** decompresses specified `.bz2` files and displays the contents without creating a separate decompressed file.

### Syntax

```shell
bzcat [parameters]
```

### Parameters

.bz2 compressed file: Specify the `.bz2` file whose contents are to be displayed.

### Examples

Compress `/tmp/man.config` using bzip2 format:

```shell
bzip2 -z man.config
```

At this point, `man.config` becomes `man.config.bz2`.

Read the contents of the compressed file:

```shell
bzcat man.config.bz2
```

The contents of `man.config.bz2` after decompression will be displayed on the screen.
