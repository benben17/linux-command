bzdiff
===

Compare two compressed files in .bz2 format.

## Description

The **bzdiff command** is used to directly compare the differences between files in two `.bz2` compressed packages, saving the step of decompressing them before calling the `diff` command.

### Syntax

```shell
bzdiff [parameters]
```

### Parameters

* File 1: Specify the first `.bz2` compressed package to compare.
* File 2: Specify the second `.bz2` compressed package to compare.
