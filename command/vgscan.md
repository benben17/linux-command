vgscan
===

Scan and display volume groups in the system.

## Description

The **vgscan command** searches for existing LVM volume groups in the system and displays a list of the groups found. The vgscan command only displays the names and LVM metadata types of the volume groups found; to get detailed information about a volume group, the vgdisplay command must be used.

### Syntax

```shell
vgscan (option)
```

### Options

```shell
-d: Debug mode;
--ignorerlockingfailure: Ignore errors related to locking failures.
```

### Examples

Use the vgscan command to scan all volume groups in the system. Enter the following command at the command line:

```shell
[root@localhost ~]# vgscan     # Scan and display the list of LVM volume groups
```

The output information is as follows:

```shell
Found volume group "vg2000" using metadata type lvm2  
Found volume group "vg1000" using metadata type lvm2 
```

Note: In this example, the vgscan command found two LVM2 volume groups, "vg1000" and "vg2000".
