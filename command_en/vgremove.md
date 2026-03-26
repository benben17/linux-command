vgremove
===

Used to delete LVM volume groups.

## Description

The **vgremove command** is used to delete LVM volume groups. If logical volumes have already been created on the volume group to be deleted, the vgremove command requires confirmation to prevent accidental data loss.

### Syntax

```shell
vgremove (option) (parameter)
```

### Options

```shell
-f: Force deletion.
```

### Parameters

Volume Group: Specifies the name of the volume group to be deleted.

### Examples

Use the vgremove command to delete LVM volume group "vg1000". Enter the following command at the command line:

```shell
[root@localhost ~]# vgremove vg1000    # Delete volume group "vg1000"
Volume group "vg1000" successfully removed
```
