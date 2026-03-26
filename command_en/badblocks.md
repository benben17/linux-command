badblocks
===

Search for bad blocks on a disk device.

## Description

The **badblocks command** is used to search for bad blocks on a disk device. A hard drive is a consumable device that may develop physical failures such as bad sectors after being used for a period of time. If bad sectors appear on a computer's hard drive and are not replaced or technically treated in time, the number of bad sectors will increase, leading to frequent system crashes and data loss. The best way to handle this is to replace the disk, but in temporary situations, the sectors in the bad parts should be masked in time and not touched. `badblocks` is an excellent tool for checking the location of bad sectors.

### Syntax

```shell
badblocks [options] [parameters]
```

### Options

```shell
-b <block_size>: Specify the block size of the disk in bytes.
-o <output_file>: Write the results of the check to the specified output file.
-s: Show progress during the check.
-v: Display detailed information during execution.
-w: Perform a write test during the check.
```

### Parameters

* Disk device: Specify the disk device to be checked.
* Number of blocks: Specify the total number of blocks on the disk device.
* Start block: Specify the block from which to start the check.

### Examples

`badblocks` checks each block 16 times with a block size of 4096 and outputs the result to the "hda-badblocks-list" file.

```shell
badblocks -b 4096 -c 16 /dev/hda1 -o hda-badblocks-list
```

`hda-badblocks-list` is a text file with the following content:

```shell
cat hda-badblocks-list
51249
51250
51251
51253
51254
……
61245
……
```

You can perform multiple operations on suspicious blocks. Below, `badblocks` uses a block size of 4096 bytes, checks each block once, and outputs the result to the "hda-badblocks-list.1" file, starting from block 51000 and ending at block 63000.

```shell
badblocks -b 4096 -c 1 /dev/hda1 -o hda-badblocks-list.1 63000 51000
```

This operation takes a relatively short time, and the hard drive might produce a clicking sound in a very short time under the specified conditions. Since the check conditions are different, the output results are not exactly the same. Repeating the same operation several times will yield different results because the conditions vary slightly. After performing multiple operations, the final `hda-badblock-list.final` file is generated.

### Others

**1. Using badblocks information with fsck**

`badblocks` only marks the information of bad sectors in the log file. If you want to skip these bad blocks when checking the disk, you can use the `-l` parameter of `fsck`:

```shell
fsck.ext3 -l /tmp/hda-badblock-list.final /dev/hda1
```

**2. Checking for bad sectors before creating a file system**

`badblocks` can be run together with the `-c` option of `e2fsck` and `mke2fs` (the same applies to the ext3 file system) to detect bad sector information before creating the file system:

```shell
mkfs.ext3 -c /dev/hda1
```

The code indicates using `-c` to check for bad blocks on the hard drive before creating the file system.

This operation clearly informs us that we can use the `mkfs.ext3 -c` option to check the hard drive in read-only mode. This command checks the hard drive while formatting it and marks any faulty blocks. Formatting a hard drive this way requires considerable patience because the command checks the hard drive block by block.
