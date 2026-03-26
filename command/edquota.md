edquota
===

Edit user or group disk quotas.

## Description

The **edquota** command is used to edit disk quotas for a specified user or group. By default, `edquota` uses `vi` to edit the quota settings for users or groups.

### Syntax

```shell
edquota [options] [parameters]
```

### Options

```shell
-u: Set user quota (default).
-g: Set group quota.
-p <source user>: Apply the quota settings of the source user to other users or groups.
-t: Set grace period.
```

### Parameters

User: Specify the username or group name for which to edit disk quota limits.

### Examples

**Configuring System Disk Quota Support**

First, disk quotas are partition-specific. You can decide which partition to apply disk quotas to. Generally, for a web hosting server, `/home` and `/www` (or similar) are partitions for users to store resources, so disk quotas can be applied to these two partitions. Suppose we need to implement user-level limits for the `/home` partition and group-level limits for `/www`.

Step 1:

```shell
vi /etc/fstab
```

Find the lines corresponding to `/home` and `/www`, for example:

```shell
/dev/sda5 /home ext2 defaults 1 2
/dev/sda7 /www ext2 defaults 1 2
```

To implement user-level disk quotas for `/home`, modify the mount options for the `sda5` line as follows:

```shell
/dev/sda5 /home ext2 defaults,usrquota 1 2
```

Note that it's `usrquota`. Similarly, we can modify the `/www` line as follows:

```shell
/dev/sda7 /www ext2 defaults,grpquota 1 2
```

For the root user, edit `/etc/fstab`:

```shell
LABEL=/ / ext2 defaults,usrquota,grpquota 1 1
```

Description: Each line of the `/etc/fstab` file consists of six fields:

*   Field 1: File system (partition) comment (similar to a label).
*   Field 2: Mount point of the file system.
*   Field 3: File system type (disk quotas can only be implemented on ext2/ext3/ext4 file systems).
*   Field 4: Mount options. Add the `usrquota` keyword for user-based quotas, `grpquota` for group-based quotas, or both separated by a comma.
*   Field 5: Indicates if the file system is read-only (0) or read-write (1).
*   Field 6: Order in which `fsck` checks the file system at boot.

Note: Please pay attention to the spelling: `usrquota` and `grpquota`, not `userquota` or `groupquota`.

Enter single-user mode and use `quotacheck` to generate `.user` or `.group` files:

```shell
quotacheck / ; quotacheck /home
```

If single-user mode throws an error, `umount` your device `/dev/hda*` first, then execute it. Restart the system, and if everything is normal, quotas will start working.

**Setting Quota Allocations for Users and Groups**

Disk quota limits are generally implemented from two aspects: the disk space occupied by a user and the total number of files. Before the specific operation, let's understand two basic concepts: soft limit and hard limit.

*   Soft limit: The maximum disk space and maximum number of files a user can have on the file system. This limit can be temporarily exceeded within a certain grace period.
*   Hard limit: The absolute maximum disk space or number of files a user can have. Exceeding this limit is strictly prohibited.

**Editing Quota Data Files via edquota:**

Use the `edquota` command to configure quotas for users after restarting the system. Assuming `lanf` is the system account that needs a quota, use the following command:

```shell
edquota -u lanf
```

This command will launch the default text editor (such as `vi` or another editor specified by the `$EDITOR` environment variable) with content similar to:

```shell
Quotas for user lanf:
/dev/sda5:blocks in use:0,limits(soft = 0,hard = 0)
inodes in use:0,limits(soft = 0,hard = 0)
```

This indicates that the user `lanf` has used 0 blocks (in KB) in the `/dev/sda5` partition (which is already under `usrquota` control) and has no limits (soft or hard). Similarly, `lanf` has no files or directories in this partition and no inode limits. If we want to limit the user's disk capacity, we only need to modify the `limits` part of the `blocks` line. Note that the unit is KB. For example, to assign a 100MB soft limit and 400MB hard limit for `lanf`:

```shell
Quotas for user lanf:
/dev/sda5:blocks in use:0,limits(soft = 102400,hard = 409800)
inodes in use:0,limits(soft = 0,hard = 0)
```

Similarly, to limit the number of files/directories, modify the `inodes` line. You can also limit both. For example:

```shell
/dev/sda5:blocks in use:0,limits(soft = 102400,hard = 409800)
inodes in use:0,limits(soft = 12800,hard = 51200)
```

This means that in addition to the capacity limits, a soft limit of 12,800 and a hard limit of 51,200 have been placed on the number of files/directories. After saving the new configuration, the user's disk usage cannot exceed the hard limit. If the user tries to exceed this limit, the operation will be cancelled and an error message will be received.

If you need to set quotas for many users, the `-p` (prototype) parameter can copy the settings of an existing user. For example, to apply the same quota configuration as `lanf` to users `Jack`, `Tom`, and `Chen`:

```shell
edquota -p lanf -u Jack Tom Chen
```

For group quotas, change the `-u` option to `-g`. For example:

```shell
edquota -g webterm1
```

Actually, the above limits only affect hard limits. To make soft limits effective, you need to set a grace period. The default grace period for soft limits is infinite. You can use the `-t` option of the `edquota` command:

```shell
edquota -t
```

It will display something like:

```shell
time units may be:days,hours,minutes,or seconds
Grace period before enforcing soft limits for users:
/dev/sda5:block grace period:0 days,file grace period:0 days
```

You can set the grace period in units of days, hours, minutes, or seconds. For example:

```shell
Time units may be:days,hours,minutes,or seconds
Grace period before enforcing soft limits for users:
/dev/sda5:block grace period:2 days,file grace period:6 hours
```

**Adding Quotas via setquota:**

For example, to add a disk quota for user `bye2000`, execute:

```shell
setquota –u / 2000 2500 100 110 bye2000
```

Syntax of the `setquota` command:

```shell
setquota [ -u|-g ] mount_point soft_blocks hard_blocks soft_inodes hard_inodes user/group
```

**Viewing User Disk Usage**

To find out how much disk space a specific user (e.g., `lanf`) has used:

```shell
quota -u lanf
```

Output:

```shell
Disk quotas for user lanf(uid 503):
Filesystem blocks quota limit grace file quota limit grace
/dev/sda5 3 102400 409800 1 12800 51200
```

Similarly, use `quota -g groupname` to view group usage.

Note:
1. If no quota is configured for the user, it displays `Disk quotas for user lanf (uid 503): none`.
2. Running `quota` without any parameters shows your own quota usage.
