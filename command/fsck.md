fsck
===

Check and repair a Linux filesystem.

## Description

The **fsck command** (file system check) is used to check and, if necessary, repair one or more Linux filesystems. It is often run automatically during system boot if a filesystem was not unmounted cleanly.

### Syntax

```shell
fsck (options) (parameters)
```

### Options

```shell
-a: Automatically repair the filesystem without asking any questions.
-A: Check all filesystems listed in /etc/fstab.
-N: Do not execute; just show what would be done.
-P: When used with "-A", check all filesystems in parallel.
-r: Interactive mode; prompt for confirmation before making repairs.
-R: When used with "-A", skip the root filesystem.
-s: Serialize fsck operations (check one by one instead of in parallel).
-t <type>: Specify the type of filesystem to be checked.
-T: Do not show the title on startup.
-V: Produce verbose output, showing command execution details.
```

### Parameters

Filesystem: Specifies the device or mount point of the filesystem to be checked.

### Examples

If a Linux system shuts down abnormally, it may lead to filesystem corruption. If the system identifies a specific partition with errors, such as `/dev/hda2`, you can use the following command to attempt a repair:

```shell
fsck -y /dev/hda2
```

After the command completes, use the `reboot` command to restart the system.

If you don't know which partition has the problem, you can simply run:

```shell
fsck
```

Enter `y` at the subsequent confirmation prompts. Once finished, reboot the system.
