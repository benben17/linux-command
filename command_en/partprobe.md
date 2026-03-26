partprobe
===

Inform the OS kernel of partition table changes without rebooting.

## Description

The **partprobe command** is used to re-read the partition table. When a partition is modified (e.g., using `fdisk`), the kernel might still use the old partition table. `partprobe` allows the kernel to recognize the changes without requiring a system reboot.

### Syntax

```shell
partprobe [options] [device]
```

### Options

```shell
-d, --dry-run   # Do not update the kernel.
-s, --summary   # Show a summary of devices and their partitions.
-h, --help      # Display help information.
-V, --version   # Display version information.
```

### Parameters

**Device**: The device file corresponding to the hard disk whose partition table needs to be re-read (e.g., `/dev/sda`).

### Examples

Add a new disk partition without rebooting the system. Suppose the host has a hard drive larger than 300GB, but currently only 3 primary partitions totaling less than 70GB are used.

```shell
[root@localhost ~]# df -h 
Filesystem Size Used Avail Use% Mounted on 
/dev/sda1 29G 3.7G  24G 14% / 
/dev/sda2 29G  22G 5.2G 81% /oracle 
tmpfs    2.0G    0 2.0G  0% /dev/shm
```

Check the current partitions:

```shell
[root@localhost ~]# cat /proc/partitions
major minor  #blocks  name

   8     0  311427072 sda
   8     1   30716248 sda1
   8     2   30716280 sda2
   8     3    8193150 sda3
   8    16     976896 sdb
   8    32     976896 sdc
...
```

Now, we need to add 100GB of space for data files without affecting current services. Use `fdisk` and `partprobe` to add a new partition without rebooting.

**Step 1: Add a new disk partition**

```shell
[root@localhost ~]# fdisk /dev/sda
...
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
p
Selected partition 4
First cylinder (8669-38770, default 8669):
Using default value 8669
last cylinder or +size or +sizeM or +sizeK (8669-38770, default 38770): +100G   
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.

WARNING: Re-reading the partition table failed with error 16: Device or resource busy.
The kernel still uses the old table.
The new table will be used at the next reboot.
Syncing disks.
```

**Step 2: Use `partprobe` to let the kernel read the new partition information**

```shell
[root@localhost ~]# partprobe
```

Using `fdisk` alone only writes the information to the disk. Normally, you would need to reboot for the kernel to see the new partition before you can format it with `mkfs`. `partprobe` forces the kernel to re-scan, avoiding the reboot.

**Step 3: Format the filesystem**

```shell
[root@localhost ~]# mkfs.ext3 /dev/sda4
...
```

**Step 4: Mount the new partition `/dev/sda4`**

```shell
[root@localhost ~]# e2label /dev/sda4 /data
[root@localhost ~]# mkdir /data
[root@localhost ~]# mount /dev/sda4 /data
[root@localhost ~]# df -h
Filesystem           Size      Used Available Use% Mounted on
/dev/sda1             29G   3.7G  24G  14% /
/dev/sda2             29G  10.8G  16G  41% /oracle
tmpfs                2.0G      0  2.0G   0% /dev/shm
/dev/sda4             92G   188M  87G   1% /data
```

Using `partprobe` allows you to create and use new partitions immediately without a system restart.
