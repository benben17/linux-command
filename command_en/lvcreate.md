lvcreate
===

Create a logical volume in an existing volume group

## Description

The **lvcreate command** is used to create a new logical volume in an existing volume group. Logical volumes are created on top of volume groups. The device files for logical volumes are stored in the volume group directory. For example, if you create a logical volume named "lvol0" in a volume group named "vg1000", the corresponding device file will be `/dev/vg1000/lvol0`.

### Syntax

```shell
lvcreate [OPTION]... [VOLUME_GROUP]
```

### Options

```shell
-n, --name: Specify the name for the new logical volume.
-L, --size: Specify the size of the logical volume. Units can be kKmMgGtT.
-l, --extents: Specify the size of the logical volume in terms of logical extents (LE).
```

### Parameters

Logical Volume: The name of the logical volume to be created.

### Examples

Create a 200MB logical volume named "lvol0" in the volume group "vg1000":

```shell
[root@localhost ~]# lvcreate -L 200M -n lvol0 vg1000
```

Output:

```shell
Logical volume "lvol0" created
```

Note: After successful creation, the new logical volume "lvol0" can be accessed via the device file `/dev/vg1000/lvol0`.
