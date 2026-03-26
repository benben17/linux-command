lvresize
===

Resize a logical volume

## Description

The **lvresize command** is used to resize an LVM logical volume by extending or reducing its size. Caution is advised when reducing the size of a logical volume, as it can lead to data loss.

### Syntax

```shell
lvresize [OPTION]... LOGICAL_VOLUME_PATH
```

### Options

```shell
-L, --size: Specify the new size of the logical volume. Units can be kKmMgGtT. Prefix with '+' to add or '-' to subtract from the current size.
-l, --extents: Specify the new size in logical extents (LE). Prefix with '+' to add or '-' to subtract from the current size.
```

### Parameters

Logical Volume: The path to the logical volume to be resized.

### Examples

Increase the size of a logical volume by 200MB:

```shell
[root@localhost ~]# lvresize -L +200M /dev/vg1000/lvol0
```

Output:

```shell
Extending logical volume lvol0 to 280.00 MB
Logical volume lvol0 successfully resized
```
