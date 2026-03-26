lvextend
===

Extend the size of a logical volume

## Description

The **lvextend command** allows you to extend the size of a logical volume online, without interrupting application access to the volume. This dynamic extension is transparent to applications using the logical volume.

### Syntax

```shell
lvextend [OPTION]... LOGICAL_VOLUME_PATH
```

### Options

```shell
-L, --size: Specify the new size of the logical volume. Units can be kKmMgGtT. Prefix with '+' to add to the current size.
-l, --extents: Specify the new size in logical extents (LE). Prefix with '+' to add to the current size.
```

### Parameters

Logical Volume: The path to the logical volume to be extended.

### Examples

Add 100MB of space to the logical volume `/dev/vg1000/lvol0`:

```shell
[root@localhost ~]# lvextend -L +100M /dev/vg1000/lvol0
```

Output:

```shell
Extending logical volume lvol0 to 300.00 MB  
Logical volume lvol0 successfully resized
```
