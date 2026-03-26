fdisk
===

View disk usage and manage disk partitions.

## Description

The **fdisk command** is used to observe the usage of physical hard disks and to partition them. It uses a traditional question-and-answer interface rather than an interactive interface like `cfdisk` (similar to DOS `fdisk`). While this makes it somewhat less convenient to use, its functionality is uncompromising.

### Syntax

```shell
fdisk [options] <disk>           Change partition table
fdisk [options] -l [<disk>...]   List partition table
```

### Options

```shell
Options:
 -b, --sectors-size <size>     Display sector count and size.
 -B, --protect-boot            Do not erase bootbits when creating a new label.
 -c, --compatibility[=<mode>]  Mode, either "dos" or "nondos" (default).
 -L, --color[=<when>]          Colored output (auto, always, or never). Color is enabled by default.
 -l, --list                    Display partitions and exit.
 -x, --list-details            Similar to --list but provides more details.
 -n, --noauto-pt               Do not create a default partition table on empty devices.
 -o, --output <list>           Output columns.
 -t, --type <type>             Recognize only specified partition table types.
 -u, --units[=<unit>]          Display units, "cylinders" or "sectors" (default).
 -s, --getsz                   Display device size in 512-byte sectors [deprecated].
 -b, --bytes                   Print SIZE in bytes instead of a human-readable format.
     --lock[=<mode>]           Use an exclusive device lock (yes, no, or nonblock).
 -w, --wipe <mode>             Wipe signatures (auto, always, or never).
 -W, --wipe-partitions <mode>  Wipe signatures from new partitions (auto, always, or never).

 -C, --cylinders <number>      Specify the number of cylinders.
 -H, --heads <number>          Specify the number of heads.
 -S, --sectors <number>        Specify the number of sectors per track.

 -h, --help                    Display this help message.
 -V, --version                 Display version information.
```

### Parameters

Device File: Specifies the hard disk device file to be partitioned or displayed.

### Examples

First, select the disk to operate on:

```shell
[root@localhost ~]# fdisk /dev/sdb
```

Enter `m` to list executable commands:

```shell
command (m for help): m
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition
   l   list known partition types
   m   print this menu
   n   add a new partition
   o   create a new empty DOS partition table
   p   print the partition table
   q   quit without saving changes
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit
   x   extra functionality (experts only)
```

Enter `p` to list the current partitions on the disk:

```shell
Command (m for help): p

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1           1        8001   8e  Linux LVM
/dev/sdb2               2          26      200812+  83  Linux
```

Enter `d`, then select a partition number to delete an existing partition:

```shell
Command (m for help): d
Partition number (1-4): 1

Command (m for help): d
Selected partition 2
```

Check partitions to confirm they have been deleted:

```shell
Command (m for help): print

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System

Command (m for help):
```

Enter `n` to create new disk partitions; first, create two primary partitions:

```shell
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
p    // Create primary partition
Partition number (1-4): 1  // Partition number
First cylinder (1-391, default 1):  // Partition start position
Using default value 1
last cylinder or +size or +sizeM or +sizeK (1-391, default 391): 100  // Partition end position

Command (m for help): n  // Create another partition
Command action
   e   extended
   p   primary partition (1-4)
p 
Partition number (1-4): 2  // Partition number 2
First cylinder (101-391, default 101):
Using default value 101
Last cylinder or +size or +sizeM or +sizeK (101-391, default 391): +200M  // Partition end position, in MB
```

Confirm that the partitions were created successfully:

```shell
Command (m for help): p

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         100      803218+  83  Linux
/dev/sdb2             101         125      200812+  83  Linux
```

Create an extended partition:

```shell
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
e  // Select extended partition
Partition number (1-4): 3
First cylinder (126-391, default 126):
Using default value 126
Last cylinder or +size or +sizeM or +sizeK (126-391, default 391):
Using default value 391
```

Confirm that the extended partition was created successfully:

```shell
Command (m for help): p

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         100      803218+  83  Linux
/dev/sdb2             101         125      200812+  83  Linux
/dev/sdb3             126         391     2136645    5  Extended
```

Create two logical partitions within the extended partition:

```shell
Command (m for help): n
Command action
   l   logical (5 or over)
   p   primary partition (1-4)
l // Select logical partition
First cylinder (126-391, default 126):
Using default value 126
Last cylinder or +size or +sizeM or +sizeK (126-391, default 391): +400M    

Command (m for help): n
Command action
   l   logical (5 or over)
   p   primary partition (1-4)
l
First cylinder (176-391, default 176):
Using default value 176
Last cylinder or +size or +sizeM or +sizeK (176-391, default 391):
Using default value 391
```

Confirm that the logical partitions were created successfully:

```shell
Command (m for help): p

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         100      803218+  83  Linux
/dev/sdb2             101         125      200812+  83  Linux
/dev/sdb3             126         391     2136645    5  Extended
/dev/sdb5             126         175      401593+  83  Linux
/dev/sdb6             176         391     1734988+  83  Linux

Command (m for help):
```

From the above results, we can see that on disk `sdb`, we created 2 primary partitions (`sdb1`, `sdb2`), 1 extended partition (`sdb3`), and 2 logical partitions (`sdb5`, `sdb6`).

Note: Primary and extended partition numbers are 1-4, meaning there can be at most 4 primary or extended partitions. Logical partition numbers start from 5, which is why there is no `sdb4` in this experiment.

Finally, save the partition operations:

```shell
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

After creating partitions, we need to format them before they can be used in the system.

Create an `ext2` partition on `sdb1`:

```shell
[root@localhost ~]# mkfs.ext2 /dev/sdb1
mke2fs 1.39 (29-May-2006)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
100576 inodes, 200804 blocks
10040 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=209715200
7 block groups
32768 blocks per group, 32768 fragments per group
14368 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840

Writing inode tables: done                           
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 32 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
```

Create an `ext3` partition on `sdb6`:

```shell
[root@localhost ~]# mkfs.ext3 /dev/sdb6
mke2fs 1.39 (29-May-2006)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
217280 inodes, 433747 blocks
21687 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=444596224
14 block groups
32768 blocks per group, 32768 fragments per group
15520 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912

Writing inode tables: done                           
Creating journal (8192 blocks): done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 32 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
[root@localhost ~]#
```

Create two directories `/oracle` and `/web`, and mount the two new partitions to the system:

```shell
[root@localhost ~]# mkdir /oracle
[root@localhost ~]# mkdir /web
[root@localhost ~]# mount /dev/sdb1 /oracle
[root@localhost ~]# mount /dev/sdb6 /web
```

Check partition mounting:

```shell
[root@localhost ~]# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/mapper/VolGroup00-LogVol00
                      6.7G  2.8G  3.6G  44% /
/dev/sda1              99M   12M   82M  13% /boot
tmpfs                 125M     0  125M   0% /dev/shm
/dev/sdb1             773M  808K  733M   1% /oracle
/dev/sdb6             1.7G   35M  1.6G   3% /web
```

To automatically mount these partitions on boot, modify the `/etc/fstab` file and add the following two lines:

```shell
[root@localhost ~]# vim /etc/fstab

/dev/VolGroup00/LogVol00 /                       ext3    defaults        1 1
LABEL=/boot             /boot                   ext3    defaults        1 2
tmpfs                   /dev/shm                tmpfs   defaults        0 0
devpts                  /dev/pts                devpts  gid=5,mode=620  0 0
sysfs                   /sys                    sysfs   defaults        0 0
proc                    /proc                   proc    defaults        0 0
/dev/VolGroup00/LogVol01 swap                    swap    defaults        0 0
/dev/sdb1               /oracle                 ext2    defaults        0 0
/dev/sdb6               /web                    ext3    defaults        0 0
```
