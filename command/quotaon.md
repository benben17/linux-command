quotaon
===

Activate the disk quota function for the specified file systems in the Linux kernel.

## Description

Executing the **quotaon** command enables disk space usage limits for users and groups. However, before enabling them, the root directory of each partition's file system must contain the quota configuration files created by the `quotacheck` command.

### Syntax

```shell
quotaon [options] [parameters]
```

### Options

```shell
-a: Enable space limits for partitions in /etc/fstab that have quota settings included.
-g: Enable disk space limits for groups.
-u: Enable disk space limits for users.
-v: Display the process of command execution (verbose mode).
```

### Parameters

File system: Specifies the file system for which the disk quota functionality should be activated.
