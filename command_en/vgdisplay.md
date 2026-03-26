vgdisplay
===

Display information about LVM volume groups.

## Description

The **vgdisplay command** is used to display information about LVM volume groups. If no "Volume Group" parameter is specified, the attributes of all volume groups are displayed.

### Syntax

```shell
vgdisplay (option) (parameter)
```

### Options

```shell
-A: Display attributes of active volume groups only;
-s: Use short format for output information.
```

### Parameters

Volume Group: The name of the volume group whose attributes are to be displayed.

### Examples

Use the vgdisplay command to show the attributes of the existing volume group "vg1000". Enter the following command at the command line:

```shell
[root@localhost ~]# vgdisplay vg1000     # Display attributes of volume group "vg1000"
```

The output information is as follows:

```shell
  --- Volume group ---  
  VG Name               vg1000  
...... (output truncated) ......  
  free PE / Size        50 / 200.00 MB  
  VG UUID               ICprwg-ZmhA-JKYF-WYuy-jNHa-AyCN-ZS5F7B
```
