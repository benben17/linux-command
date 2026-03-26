vgrename
===

Rename a volume group.

## Description

The **vgrename command** can be used to rename a volume group.

### Syntax

```shell
vgrename [options] [old_vg_path|old_vg_name|old_vg_uuid] [new_vg_path|new_vg_name]
```

### Options

```shell
-d: Enable debug mode;
-t: Enable test mode.
```

### Examples

Rename volume group `/dev/vg1` to `/dev/vg2`.

```shell
[root@localhost ~]# vgrename /dev/vg1 /dev/vg2
  Volume group "vg1" successfully renamed to "vg2"
```

Rename volume group `vg1` to `vg2`.

```shell
[root@localhost ~]# vgrename vg1 vg2
  Volume group "vg1" successfully renamed to "vg2"
```
