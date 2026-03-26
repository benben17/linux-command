pvscan
===

Scan all disks in the system for a list of physical volumes.

## Description

The **pvscan command** scans all connected hard disks in the system and lists the physical volumes found. Using the `-n` option displays physical volumes that do not belong to any volume group, which are currently unused.

### Syntax

```shell
pvscan(options)
```

### Options

```shell
-d: Debug mode;
-e: Only show physical volumes belonging to exported volume groups;
-n: Only show physical volumes that do not belong to any volume group;
-s: Short format output;
-u: Display UUIDs.
```

### Example

Scan all disks in the current system for physical volumes by entering the following command:

```shell
[root@localhost ~]# pvscan     # Scan all disks for physical volumes 
```

Output information:

```shell
PV /dev/sdb1         lvm2 [101.94 MB]  
PV /dev/sdb2         lvm2 [101.98 MB]  
Total: 2 [203.92 MB] / in use: 0 [0   ] / in no VG: 2 [203.92  
MB] 
```

Note: In this example, two physical volumes are found that do not belong to any volume group and are available for use.
