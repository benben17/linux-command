rpm2cpio
===

Convert RPM packages to cpio format files.

## Description

The **rpm2cpio command** is used to convert RPM packages into cpio format files.

### Syntax

```shell
rpm2cpio(parameter)
```

### Parameters

File: Specifies the filename of the RPM package to be converted.

### Examples

```shell
rpm2cpio ../libstdc++-4.3.0-8.i386.rpm | cpio -idv
```
