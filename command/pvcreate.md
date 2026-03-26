pvcreate
===

Initialize physical hard disk partitions as physical volumes.

## Description

The **pvcreate command** is used to initialize physical hard disk partitions as physical volumes so they can be used by LVM.

### Syntax

```shell
pvcreate(options)(parameters)
```

### Options

```shell
-f: Force the creation of a physical volume without user confirmation;
-u: Specify the UUID of the device;
-y: Answer "yes" to all questions;
-Z: Whether to utilize the first 4 sectors.
```

### Parameters

Physical Volume: Specifies the device file name corresponding to the physical volume to be created.

### Examples

View disk information:

```shell
[root@localhost ~]# fdisk -l
Disk /dev/hda: 41.1 GB, 41174138880 bytes
255 heads, 63 sectors/track, 5005 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   id  System
/dev/hda1   *           1          13      104391   83  Linux
/dev/hda2              14        1288    10241437+  83  Linux
/dev/hda3            1289        1925     5116702+  83  Linux
/dev/hda4            1926        5005    24740100    5  Extended
/dev/hda5            1926        2052     1020096   82  Linux swap / Solaris
/dev/hda6            2053        2235     1469916   8e  Linux LVM
/dev/hda7            2236        2418     1469916   8e  Linux LVM
/dev/hda8            2419        2601     1469916   8e  Linux LVM
/dev/hda9            2602        2784     1469916   8e  Linux LVM
```

Check if any PVs exist on the system, then initialize `/dev/hda6` to `/dev/hda9` as PVs:

```shell
[root@localhost ~]# pvscan
No matching physical volumes found    # No PVs found!
```

Convert partitions 6-9 to PVs (note the use of curly braces):

```shell
[root@localhost ~]# pvcreate /dev/hda{6,7,8,9}
  Physical volume "/dev/hda6" successfully created
  Physical volume "/dev/hda7" successfully created
  Physical volume "/dev/hda8" successfully created
  Physical volume "/dev/hda9" successfully created
```

Display information for each PV and summary information for all PVs:

```shell
[root@localhost ~]# pvscan
  PV /dev/hda6         lvm2 [1.40 GB]
  PV /dev/hda7         lvm2 [1.40 GB]
  PV /dev/hda8         lvm2 [1.40 GB]
  PV /dev/hda9         lvm2 [1.40 GB]
  Total: 4 [5.61 GB] / in use: 0 [0   ] / in no VG: 4 [5.61 GB]
```

Display detailed information for each PV on the system:

```shell
[root@localhost ~]# pvdisplay
  "/dev/hda6" is a new physical volume of "1.40 GB"
  --- NEW Physical volume ---
  PV Name               /dev/hda6  # Actual partition name
  VG Name                          # Blank as it's not yet assigned to a VG
  PV Size               1.40 GB    # Capacity description
  Allocatable           NO         # Whether it has been allocated
  PE Size (KByte)       0          # Size of PE in this PV
  Total PE              0          # Total number of PEs
  free PE               0          # PEs not used by LVs
  Allocated PE          0          # Number of PEs still available for allocation
  PV UUID               Z13Jk5-RCls-UJ8B-HzDa-Gesn-atku-rf2biN
....(remainder omitted)....
```

Remove a physical volume:

```shell
[root@localhost ~]# pvremove /dev/sdb2
Labels on physical volume "/dev/sdb2" successfully wiped
```

Modify physical volume attributes:

```shell
[root@localhost ~]# pvchange -x n /dev/sdb1    # Prohibit allocation of PEs on specified physical volume
Physical volume "/dev/sdb1" changed  
1 physical volume changed / 0 physical volumes not changed 
```
