repquota
===

Outputs the status of disk space limits in a report format.

## Description

The **repquota command** outputs disk quota information for a specified partition or file system in a report format.

### Syntax

```shell
repquota(options)(parameters)
```

### Options

```shell
-a: Lists the status of partitions with quota settings in the /etc/fstab file, including users and groups;
-g: Lists disk space limits for all groups;
-u: Lists disk space limits for all users;
-v: Displays all space limits for the user or group.
```

### Parameters

File system: The file system or corresponding device filename to print the report for.

### Examples

Display disk usage for all file systems:

```shell
repquota -a
```
