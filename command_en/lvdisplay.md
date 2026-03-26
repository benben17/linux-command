lvdisplay
===

Display attributes of a logical volume

## Description

The **lvdisplay command** is used to display attributes of LVM logical volumes, such as size, read/write status, and snapshot information. If the "logical volume" parameter is omitted, `lvdisplay` shows attributes for all logical volumes. Otherwise, it only shows attributes for the specified logical volume.

### Syntax

```shell
lvdisplay [LOGICAL_VOLUME_PATH]
```

### Parameters

Logical Volume: The device file path of the logical volume for which to display attributes.

### Examples

Display the attributes of a specific logical volume:

```shell
[root@localhost ~]# lvdisplay /dev/vg1000/lvol0
```

Example output:

```shell
  --- Logical volume ---  
  LV Name                /dev/vg1000/lvol0  
... (output truncated) ...
  Block device           253:0
```
