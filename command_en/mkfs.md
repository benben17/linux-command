mkfs
===

Build a Linux filesystem

## Description

The **mkfs command** is used to build a Linux filesystem on a device, usually a hard disk partition. `mkfs` itself is a front-end for the various filesystem builders (mkfs.fstype) available under Linux.

### Syntax

```shell
mkfs [OPTION]... [-t TYPE] [FS-OPTIONS] DEVICE [SIZE]
```

### Options

```shell
-t <type>：Specify the type of filesystem to be built (e.g., ext3, ext4, msdos).
-v：Produce verbose output, including all filesystem-specific commands that are executed.
-V：Display version information and exit.
-c：Check the partition for bad blocks before building the filesystem.
```

### Parameters

*   Device: The special file corresponding to the device (e.g., `/dev/sda6`).
*   Size: The number of blocks for the filesystem.

### Examples

Create an MS-DOS filesystem on `/dev/hda5`, checking for bad blocks and displaying verbose output:

```shell
mkfs -V -t msdos -c /dev/hda5

# Format a partition as ext3
mkfs -t ext3 /dev/sda6

# Format a partition as ext2
mkfs -t ext2 /dev/sda7
```
