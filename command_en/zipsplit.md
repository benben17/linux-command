zipsplit
===

Split a large zip archive into smaller ones

## Description

The **zipsplit** command is used to split a large zip archive into multiple smaller zip archives.

### Syntax

```shell
zipsplit [options] [parameters]
```

### Options

```shell
-n, --size=[size]: Specify the maximum size for each split zip file;
-t, --test: Report how many smaller zip files will be created and their sizes;
-b, --path=[path]: Specify the directory where the split zip files will be stored.
```

### Parameters

File: Specifies the zip archive to be split.
