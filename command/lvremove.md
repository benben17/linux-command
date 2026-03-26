lvremove
===

Remove a logical volume

## Description

The **lvremove command** is used to remove an LVM logical volume. If a logical volume is currently mounted, it cannot be removed. It must be unmounted using the `umount` command before it can be deleted.

### Syntax

```shell
lvremove [OPTION]... LOGICAL_VOLUME_PATH
```

### Options

```shell
-f, --force: Force removal without confirmation.
```

### Parameters

Logical Volume: The path to the logical volume to be removed.

### Examples

Remove a specific logical volume:

```shell
[root@localhost ~]# lvremove /dev/vg1000/lvol0
```

Output:

```shell
Do you really want to remove active logical 
volume "lvol0"? [y/n]: y
  Logical volume "lvol0" successfully removed
```
