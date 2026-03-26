# quotaoff

Disable the disk quota function for the specified file systems in the Linux kernel.

## Description

The **quotaoff** command is used to disable the disk quota function for specified file systems in the Linux kernel.

### Syntax

```shell
quotaoff [options] [parameters]
```

### Options

```shell
-a: Disable space limits for all partitions in /etc/fstab that have quota settings enabled.
-g: Disable group disk space limits.
-u: Disable user disk space limits.
-v: Show the process of command execution (verbose mode).
```

### Parameters

File system: Specifies the file system for which the disk quota functionality should be disabled.
