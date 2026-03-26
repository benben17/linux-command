parted
===

A tool for disk partitioning and partition resizing.

## Description

The **parted command** is a powerful disk partitioning and partition resizing tool developed by the GNU project. Unlike `fdisk`, it supports resizing partitions. Designed for Linux, it handles common partition formats including ext2, ext3, fat16, fat32, NTFS, ReiserFS, JFS, XFS, UFS, HFS, and Linux swap.

### Syntax

```shell
parted [options] [device [command [arguments...]]]
```

### Options

```shell
-h, --help      # Display help information.
-i, --interactive # Interactive mode.
-s, --script    # Script mode, no user prompting.
-v, --version   # Display version information.
```

### Parameters

*   **Device**: The device file corresponding to the hard disk to be partitioned (e.g., `/dev/sdb`).
*   **Command**: The parted command to be executed.

### Examples

With the advent of serial technology, more users are choosing large-capacity SATA hard drives to create disk arrays. In particular, MD1000/MD3000 systems easily exceed 2TB LUNs. Red Hat Enterprise Linux 4 Update 4 and later support disk devices larger than 2 terabytes (TB).

Here are the steps to partition a disk using GPT:

```shell
[root@localhost ~]# fdisk -l
...
Disk /dev/sdb: 2147 MB, 2147483648 bytes
255 heads, 63 sectors/track, 261 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Disk /dev/sdb doesn't contain a valid partition table
```

Start `parted` on the device:

```shell
[root@localhost ~]# parted /dev/sdb
GNU Parted Copyright (C) 1998 - 2004 Free Software Foundation, Inc.
...
Using /dev/sdb
(parted) mklabel gpt
(parted) print
Disk geometry for /dev/sdb: 0.000-2048.000 megabytes
Disk label type: gpt
Minor   Start       End         Filesystem  Name                  Flags
(parted) mkpart primary 0 2048  # Use the numbers shown in the print output
(parted) print
Disk geometry for /dev/sdb: 0.000-2048.000 megabytes
Disk label type: gpt
Minor   Start       End         Filesystem  Name                  Flags
1       0.017       2047.983
(parted) quit
```

Don't forget to update `/etc/fstab` if necessary.

Verify with `fdisk -l`:

```shell
[root@localhost ~]# fdisk -l
...
WARNING: GPT (GUID Partition Table) detected on '/dev/sdb'! The util fdisk doesn't support GPT. Use GNU Parted.

Disk /dev/sdb: 2147 MB, 2147483648 bytes
...
   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         262     2097151+  ee  EFI GPT
```

Format the new partition:

```shell
[root@localhost ~]# mkfs.ext3 /dev/sdb1
...
```

Mount and check the disk space:

```shell
[root@localhost ~]# mount /dev/sdb1 /mnt
[root@localhost ~]# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/sda3              32G  2.6G   28G   9% /
/dev/sda1              99M   12M   82M  13% /boot
none                  252M     0  252M   0% /dev/shm
/dev/sdb1             2.0G   36M  1.9G   2% /mnt
```
