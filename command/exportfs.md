exportfs
===

Manage the list of NFS shared file systems.

## Description

The **exportfs** command is used to manage the current list of NFS shared file systems.

### Options

```shell
-a: Share or unshare all directories.
-o options,...: Specify a list of share options, similar to those in exports(5).
-i: Ignore the /etc/exports file; only use default and command-line options.
-r: Re-share all directories. It synchronizes /var/lib/nfs/xtab with /etc/exports. It removes deleted entries from /var/lib/nfs/xtab and removes any entries that are no longer valid from the kernel share table.
-u: Unshare one or more directories.
-f: Flush the kernel share table in "new" mode. Active clients will receive new share entries from mountd on their next request.
-v: Be verbose. Show what is being shared or unshared. When listing shares, also display the share options.
```
