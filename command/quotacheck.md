quotacheck
===

Check disk usage and limits.

## Description

The **quotacheck command** scans a specified filesystem for disk usage and creates, checks, and repairs disk quota files. It scans partitions and generates `aquota.user` and `aquota.group` files in the root of each filesystem to set disk space limits for users and groups.

If you see the following message when running `quotacheck`:

```shell
quotacheck: Your kernel probably supports journaled quota but you are not using it. Consider switching to journaled quota to avoid running quotacheck after an unclean shutdown. 
```

Consider updating your filesystem configuration to use: `usrjquota=aquota.user,grpjquota=aquota.group,jqfmt=vfsv1`, then remount the filesystem: `mount -vo remount /mount/point`. (Caution: If issues arise during this step, do not reboot; revert the configuration instead.)

### Syntax

```shell
quotacheck(options)(parameters)
```

### Options

```shell
-a: Scan all partitions in /etc/fstab that have quota enabled;
-c: Perform a new scan and create new quota files;
-d: Display detailed execution process for troubleshooting;
-g: Calculate the number of directories and files for each group;
-R: Exclude the root partition from scanning;
-u: Calculate the number of directories and files for each user;
-v: Display the execution process.
```

### Parameters

Filesystem: Specifies the filesystem to be scanned.

### Example

Scan all partitions in `/etc/mtab` that support quotas:

```shell
[root@linux ~]# quotacheck -avug
quotacheck: Scanning /dev/hdb1 [/disk2] done
quotacheck: Checked 3 directories and 4 files
```

Force scan of a mounted filesystem:

```shell
[root@linux ~]# quotacheck -avug -m
```

Scan a specific filesystem:

```shell
[root@linux ~]# quotacheck -cvug /disk2
```
