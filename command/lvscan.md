lvscan
===

Scan for logical volumes

## Description

The **lvscan command** scans all LVM logical volumes in the system and displays them along with their device files.

### Syntax

```shell
lvscan [OPTION]...
```

### Options

```shell
-b：Show the major and minor device numbers of the logical volumes.
```

### Examples

Scan for all logical volumes in the system:

```shell
[root@localhost ~]# lvscan
```

Example output:

```shell
ACTIVE          '/dev/vg1000/lvol0' [200.00 MB] inherit
```
