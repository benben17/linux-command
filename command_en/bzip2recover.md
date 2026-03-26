bzip2recover
===

Recovers data from damaged .bz2 files.

## Description

The **bzip2recover command** can be used to recover files from damaged `.bz2` compressed packages.

`bzip2` compresses files in blocks, with each block treated as an independent unit. Therefore, when a certain block is damaged, `bzip2recover` can be used to try and separate the blocks in the file so that the normal blocks can be decompressed. This is usually only applicable when the compressed file is very large.

### Syntax

```shell
bzip2recover [parameters]
```

### Parameters

File: Specify the `.bz2` compressed package from which data is to be recovered.
