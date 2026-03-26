quota
===

Display disk usage and limits.

## Description

The **quota command** is used to display disk quota information for a user or group. The output includes current disk usage and the defined quota limits.

### Syntax

```shell
quota(options)(parameters)
```

### Options

```shell
-g: List disk space limits for groups;
-q: Brief format, only listing components that exceed limits;
-u: List disk space limits for users;
-v: Display space limits for the user or group on all mounted filesystems;
-V: Display version information.
```

### Parameters

User or Group: Specifies the user or group whose quota information is to be displayed.

### Example

You can restrict the maximum disk quota for a group and further restrict the quota for an individual user. For instance, in a paid application, VIP users could be granted more space. Additionally, by using symbolic links, you can set a quota for mail by pointing `/var/spool/mail` to a directory on a disk where quotas are enabled (like `/home`). This is useful when the initial disk planning was insufficient but you don't want to change the existing architecture.

Requirement: Implement disk quotas for users `quser1` and `quser2`, both of whom belong to the `qgroup` group. Each user is limited to 50MB (ignoring inodes), with a soft limit of 45MB. The grace period is set to 1 day; excess files must be deleted within this timeframe, or the remaining space will become unavailable. The `qgroup` group has a maximum limit of 90MB. (Note: This flexible setup is common in mail services where total promised space exceeds physical capacity, as not all users use their full quota.)

```shell
[root@localhost ~]# groupadd qgroup
[root@localhost ~]# useradd -m -g qgroup quser1
[root@localhost ~]# useradd -m -g qgroup quser2
[root@localhost ~]# passwd quser1
[root@localhost ~]# passwd quser2
[root@localhost ~]# df     # Find a suitable partition; using /disk2 here
Filesystem             1K-blocks        Used      Available   Use% Mounted on
/dev/hda1              5952252   3193292     2451720     57%     /
/dev/hdb1            28267608       77904   26730604       1%     /disk2
/dev/hda5              9492644     227252     8775412       3%     /disk1

[root@localhost ~]# vi /etc/fstab
LABEL=/             /                ext3      defaults                                     1 1
LABEL=/disk1    /disk1        ext3      defaults                                      1 2
LABEL=/disk2    /disk2        ext3      defaults,usrquota,grpquota       1 2  
/dev/hda3         swap         swap     defaults                                     0 0
```

Note the addition of `usrquota,grpquota` without spaces. Since quotas are read from `/etc/mtab`, which is updated upon reboot from `/etc/fstab`, you should reboot or remount the filesystem.

Remount the filesystem to activate settings:

```shell
[root@localhost ~]# umount /dev/hdb1
[root@localhost ~]# mount -a
[root@localhost ~]# grep '/disk2' /etc/mtab
/dev/hdb1 /disk2 ext3 rw,usrquota,grpquota 0 0
```

Alternatively, use the remount option:

```shell
[root@localhost ~]# mount -o remount /disk2
```

Now the quota feature is successfully added to the filesystem.

Scan disk usage and generate `aquota.group` and `aquota.user` files:

```shell
[root@localhost ~]# quotacheck -avug
quotacheck: Scanning /dev/hdb1 [/disk2] done
quotacheck: Checked 3 directories and 4 files

[root@localhost ~]# ll /disk2
-rw-------  1 root root  6144 Sep  6 11:44 aquota.group
-rw-------  1 root root  6144 Sep  6 11:44 aquota.user
```

Use symbolic links if your Linux version expects `quota.user` instead of `aquota.user`:

```shell
[root@localhost ~]# cd /disk2
[root@localhost ~]# ln -s aquota.user quota.user
[root@localhost ~]# ln -s aquota.group quota.group
```

Turn on quotas:

```shell
[root@localhost ~]# quotaon -avug
/dev/hdb1 [/disk2]: group quotas turned on
/dev/hdb1 [/disk2]: user quotas turned on    # "turned on" indicates success!
```

Edit user space limits:

```shell
[root@localhost ~]# edquota -u quser1
Disk quotas for user quser1 (uid 502):
  Filesystem    blocks    soft    hard   inodes   soft   hard
  /dev/hdb1           0     45000    50000         0      0      0
[root@localhost ~]# edquota -p quser1 quser2      # Copy settings to quser2
```

Set the grace period using `edquota`:

```shell
[root@localhost ~]# edquota -t
Grace period before enforcing soft limits for users:
time units may be: days, hours, minutes, or seconds
  Filesystem             Block grace period     Inode grace period
  /dev/hdb1                     1days                  7days
```

Query with `quota -v`:

```shell
[root@localhost ~]# quota -vu quser1 quser2
Disk quotas for user quser1 (uid 502):
     Filesystem  blocks   quota      limit   grace   files   quota   limit   grace
      /dev/hdb1         0    45000    50000                   0       0       0
Disk quotas for user quser2 (uid 503):
     Filesystem  blocks   quota      limit   grace   files   quota   limit   grace
      /dev/hdb1         0    45000    50000                   0       0       0
```

Note: The `grace` period field remains empty until the soft limit of 45MB is exceeded.

Edit group space limits:

```shell
[root@localhost ~]# edquota -g qgroup
Disk quotas for group qgroup (gid 502):
  Filesystem     blocks       soft       hard    inodes   soft   hard
  /dev/hdb1            0      80000   90000           0      0      0

[root@localhost ~]# quota -vg qgroup
Disk quotas for group qgroup (gid 502):
     Filesystem   blocks    quota      limit      grace    files   quota   limit   grace
      /dev/hdb1         0     80000   90000                       0        0        0
```
