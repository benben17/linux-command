vgcreate
===

Used to create LVM volume groups.

## Description

The **vgcreate command** is used to create LVM volume groups. A volume group (VG) organizes multiple physical volumes into a single entity, shielding the details of the underlying physical volumes. When creating logical volumes on a volume group, specific physical volume information does not need to be considered.

### Syntax

```shell
vgcreate (option) (parameter)
```

### Options

```shell
-l: Maximum number of logical volumes allowed in the volume group;
-p: Maximum number of physical volumes allowed in the volume group;
-s: PE (Physical Extent) size for the physical volumes in the volume group.
```

### Parameters

*   Volume Group Name: The name of the volume group to be created;
*   Physical Volume List: The list of physical volumes to be added to the volume group.

### Examples

Use the vgcreate command to create a volume group named "vg1000" and add physical volumes `/dev/sdb1` and `/dev/sdb2` to it. Enter the following command at the command line:

```shell
[root@localhost ~]# vgcreate vg1000 /dev/sdb1 /dev/sdb2  # Create volume group "vg1000"
```

The output information is as follows:

```shell
Volume group "vg1000" successfully created
```
