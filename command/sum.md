sum
===

Calculate file checksums and block counts

## Description

The **sum command** is used to calculate and display the checksum and the number of disk blocks for specified files.

### Syntax

```shell
sum (options) (parameters)
```

### Options

```shell
-r: Use the BSD checksum algorithm with a block size of 1k.
-s: Use the System V checksum algorithm with a block size of 512 bytes.
```

### Parameters

File list: List of files for which to calculate the checksum and disk blocks.

### Examples

Calculate file checksum:

```shell
[root@localhost ~]# sum insert.sql
00827    12
```
