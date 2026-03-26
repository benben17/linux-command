mke2fs
===

Create an ext2, ext3, or ext4 filesystem

## Description

The **mke2fs command** is used to create an ext2, ext3, or ext4 filesystem, usually on a disk partition.

### Syntax

```shell
mke2fs [OPTION]... DEVICE [BLOCKS-COUNT]
```

### Options

```shell
-b <block-size>：Specify the size of blocks in bytes.
-c：Check the device for bad blocks before creating the filesystem.
-f <fragment-size>：Specify the size of fragments in bytes.
-F：Force mke2fs to run, even if the specified device is not a partition on a block special device.
-i <bytes-per-inode>：Specify the bytes/inode ratio.
-N <number-of-inodes>：Overrides the default calculation of the number of inodes that should be reserved for the filesystem.
-l <filename>：Read the bad blocks list from <filename>.
-L <volume-label>：Set the volume label for the filesystem.
-m <reserved-blocks-percentage>：Specify the percentage of the filesystem blocks reserved for the super-user. Default is 5%.
-M <last-mounted-directory>：Set the last mounted directory for the filesystem.
-q：Quiet execution; do not show any output.
-r <revision>：Set the filesystem revision for the new filesystem.
-R <raid-options>：Set RAID-related options.
-S：Write only the superblock and group descriptors. Useful for recovering from corruption.
-v：Verbose execution; show detailed information.
-V：Print the version number and exit.
```

### Parameters

*   Device: The special file corresponding to the device (e.g., `/dev/hda1`).
*   Blocks-count: The number of blocks on the device.

### Examples

Create an ext2 filesystem on `/dev/hda1` quietly:

```shell
mke2fs -q /dev/hda1
```
