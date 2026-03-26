bzcmp
===

Compare two compressed files in .bz2 format.

## Description

The **bzcmp command** is primarily used to compare files within two `.bz2` compressed packages without actually decompressing them, saving the step of calling the `cmp` command after decompression.

### Syntax

```shell
bzcmp [parameters]
```

### Parameters

* File 1: Specify the first `.bz2` compressed package to compare.
* File 2: Specify the second `.bz2` compressed package to compare.
