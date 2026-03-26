vgconvert
===

Convert volume group metadata format.

## Description

The **vgconvert command** is used to convert the metadata format of a specified LVM volume group, typically from "LVM1" format to "LVM2" format. Before converting the metadata, the volume group must be in an inactive state; otherwise, the conversion cannot be completed.

### Syntax

```shell
vgconvert (option) (parameter)
```

### Options

```shell
-M: The volume group format to convert to.
```

### Parameters

Volume Group: Specifies the volume group to be converted.

### Examples

Before converting the metadata format, use the vgchange command to set the volume group to an inactive state. Enter the following command at the command line:

```shell
[root@localhost lvm]# vgchange -an vg1000    # Set volume group status to inactive
0 logical volume(s) in volume group "vg1000" now active
```

Use the vgconvert command to convert the volume group "vg1000" from "LVM1" format to "LVM2" format. Enter the following command at the command line:

```shell
[root@localhost lvm]# vgconvert -M2 vg1000    # Convert volume group to "LVM2" format
Volume group vg1000 successfully converted
```

Use the vgchange command to set the volume group back to an active state. Enter the following command at the command line:

```shell
[root@localhost lvm]# vgchange -ay vg1000     # Set volume group status to active
0 logical volume(s) in volume group "vg1000" now active
```
