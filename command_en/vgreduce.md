vgreduce
===

Remove physical volumes from a volume group.

## Description

The **vgreduce command** reduces the capacity of an LVM volume group by removing physical volumes from it. You cannot remove the last remaining physical volume in an LVM volume group.

### Syntax

```shell
vgreduce (option) (parameter)
```

### Options

```shell
-a: If no physical volumes are specified on the command line, remove all empty physical volumes;
--removemissing: Remove missing physical volumes from the volume group to restore it to a normal state.
```

### Parameters

*   Volume Group: Specifies the name of the volume group to be operated on;
*   Physical Volume List: Specifies the list of physical volumes to be removed.

### Examples

Use the vgreduce command to remove physical volume `/dev/sdb2` from the volume group "vg2000". Enter the following command at the command line:

```shell
[root@localhost ~]# vgreduce vg2000 /dev/sdb2    # Remove physical volume "/dev/sdb2" from volume group "vg2000"
```

The output information is as follows:

```shell
Removed "/dev/sdb2" from volume group "vg2000"
```
