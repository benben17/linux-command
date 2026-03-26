vgchange
===

Change volume group attributes.

## Description

The **vgchange command** is used to change the attributes of a volume group, often to set it as active or inactive. An active volume group cannot be deleted; it must be set to an inactive state using the vgchange command before it can be removed.

### Syntax

```shell
vgchange (option) (parameter)
```

### Options

```shell
-a: Set the active state of the volume group.
```

### Parameters

Volume Group: Specifies the volume group whose attributes are to be set.

### Examples

Use the vgchange command to set the volume group status to active. Enter the following command at the command line:

```shell
[root@localhost ~]# vgchange -ay vg1000     # Set volume group "vg1000" to active state
```

The output information is as follows:

```shell
1 logical volume(s) in volume group "vg1000" now active
```
