chattr
===

Change file attributes on a Linux file system.

## Description

The **chattr command** is used to change file attributes. This command can modify the attributes of files or directories stored on an ext2/ext3/ext4 file system. There are 8 main modes for these attributes:

### Syntax

```shell
chattr [options]
```

### Options

```shell
a: Append only - the file can only be opened in append mode for writing.
b: Do not update the last access time of the file or directory.
c: Compressed - the file or directory is stored in a compressed format.
d: No dump - the file or directory is excluded from backup operations.
i: Immutable - the file or directory cannot be modified in any way.
s: Secure deletion - the file or directory is securely deleted.
S: Synchronous updates - the file or directory is updated immediately.
u: Undeletable - prevents accidental deletion.
```

```shell
-R: Recursively process all files and subdirectories within the specified directory.
-v <version_number>: Set the file or directory version.
-V: Display the execution process of the command.
+ <attribute>: Enable the specified attribute for the file or directory.
- <attribute>: Disable the specified attribute for the file or directory.
= <attribute>: Set the specified attribute for the file or directory.
```

### Examples

Use the `chattr` command to prevent a critical system file from being modified:

```shell
chattr +i /etc/fstab
```

Attempts to use `rm`, `mv`, or `rename` on this file will result in an "Operation not permitted" error.

Make a file append-only, so it can be added to but not deleted (useful for some log files):

```shell
chattr +a /data1/user_act.log
```
