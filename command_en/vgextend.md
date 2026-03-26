vgextend
===

Add physical volumes to a volume group.

## Description

The **vgextend command** is used to dynamically expand LVM volume groups by adding physical volumes to increase the volume group's capacity. Physical volumes in an LVM volume group can be added when the volume group is created using the vgcreate command, or dynamically added using the vgextend command.

### Syntax

```shell
vgextend (option) (parameter)
```

### Options

```shell
-d: Debug mode;
-t: Test mode.
```

### Parameters

*   Volume Group: Specifies the name of the volume group to be operated on;
*   Physical Volume List: Specifies the list of physical volumes to be added to the volume group.

### Examples

Use the vgextend command to add physical volume `/dev/sdb2` to the volume group "vg2000". Enter the following command at the command line:

```shell
[root@localhost ~]# vgextend vg2000 /dev/sdb2     # Add physical volume "/dev/sdb2" to volume group "vg2000"
```

The output information is as follows:

```shell
Volume group "vg2000" successfully extended
```
