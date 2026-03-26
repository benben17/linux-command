lvreduce
===

Reduce the size of a logical volume

## Description

The **lvreduce command** is used to reduce the space occupied by an LVM logical volume. Reducing the size of a logical volume may result in data loss, so it is crucial to back up data and confirm the operation before proceeding.

### Syntax

```shell
lvreduce [OPTION]... LOGICAL_VOLUME_PATH
```

### Options

```shell
-L, --size: Specify the new (reduced) size of the logical volume. Units can be kKmMgGtT. Prefix with '-' to subtract from the current size.
-l, --extents: Specify the new size in logical extents (LE). Prefix with '-' to subtract from the current size.
```

### Parameters

Logical Volume: The device file path of the logical volume to be reduced.

### Examples

Reduce the size of a logical volume by 50MB:

```shell
[root@localhost ~]# lvreduce -L -50M /dev/vg1000/lvol0
```

Output:

```shell
... (output truncated) ...
Do you really want to reduce lvol0? [y/n]: y
  Reducing logical volume lvol0 to 252.00 MB  
  Logical volume lvol0 successfully resized
```
