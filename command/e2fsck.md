e2fsck
===

Used to check the integrity of ext2, ext3, or ext4 file systems.

## Description

The **e2fsck** command is used to check the integrity of ext2, ext3, or ext4 file systems. It can attempt to repair errors through appropriate options.

The return values of e2fsck and their meanings are as follows:

*   0: No error occurred.
*   1: File system error occurred and has been corrected.
*   2: File system error occurred and has been corrected.
*   4: File system error occurred but was not corrected.
*   8: Operational error occurred.
*   16: Usage or syntax error occurred.
*   128: Shared library error occurred.

### Syntax

```shell
e2fsck [options] [parameters]
```

### Options

```shell
-a: Automatically repair the file system without asking the user.
-b<superblock>: Use an alternative superblock instead of the default one.
-B<block size>: Specify the block size in bytes.
-c: Run badblocks to mark bad blocks.
-C: Write completion information to a file descriptor so that the entire check process can be monitored.
-d: Display debugging information.
-f: Force checking even if the file system seems clean.
-F: Flush the device's buffers before starting.
-l<file>: Add the blocks specified in the file to the bad block list.
-L<file>: Clear the bad block list first, then add the blocks specified in the file to the bad block list.
-n: Open the file system in read-only mode and perform a non-interactive execution, answering "no" to all questions.
-p: Automatically repair the file system without asking the user.
-r: This parameter exists for compatibility and has no actual effect.
-s: Swap the byte order if the file system's byte order is inappropriate; otherwise, do nothing.
-S: Swap the byte order regardless of the file system's byte order.
-t: Display timing information.
-v: Display detailed information during execution.
-V: Display version information.
-y: Perform a non-interactive execution, answering "yes" to all questions.
```

### Parameters

File system or partition: Specify the device file name corresponding to the file system or partition.

### Examples

Check if `/dev/sda1` has any problems and repair them automatically if found:

```shell
e2fsck -a -y /dev/sda1
```

Before executing `e2fsck` or `fsck`, please `umount` the partition first, otherwise there is a risk of damaging the file system. If you need to check and repair the root directory `/`, you need to enter single-user mode to execute it.
