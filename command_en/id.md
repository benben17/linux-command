id
===

Print real and effective user and group IDs.

## Synopsis

```shell
id [OPTION]... [USER]...
```

## Description

- Without options, prints information for the specified user ID.

## Options

```shell
-a               Compatibility option; ignored.
-Z, --context    Print only the security context of the process.
-g, --group      Print only the effective group ID.
-G, --groups     Print all group IDs.
-u, --user       Print only the effective user ID.
-z, --zero       Delimit entries with NUL characters instead of whitespace.
--help           Display help and exit.
--version        Output version information and exit.
```

The following options are valid only when used with `-u`, `-g`, or `-G`:
```shell
-n, --name    Print names instead of numbers.
-r, --real    Print real IDs instead of effective IDs.
```

## Parameters
USER (optional): One or more usernames; defaults to the current user.

## Return Value

Returns 0 on success, non-zero on failure.

## Examples

```shell
[root@localhost ~]# id
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel)
```

Explanation: User "root" has UID = 0 and GID = 0. User "root" is a member of the following groups:

* root (GID: 0)
* bin (GID: 1)
* daemon (GID: 2)
* sys (GID: 3)
* adm (GID: 4)
* disk (GID: 6)
* wheel (GID: 10)

Print username, UID, and all groups for a user:

```shell
[root@localhost ~]# id -a
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel)
```

Output all different group IDs (effective, real, and supplementary):

```shell
[root@localhost ~]# id -G
0 1 2 3 4 6 10
```

Only output the effective group ID:

```shell
[root@localhost ~]# id -g
0
```

Output information for a specific user:

```shell
[root@localhost ~]# id www
uid=500(www) gid=500(www) groups=500(www)
```

### Note

1. This command displays real and effective User IDs (UID) and Group IDs (GID). The UID is a unique identifier for a user. A GID can correspond to multiple UIDs. Some programs require specific UID/GID to run. `id` makes it easy to find these without searching `/etc/passwd` or `/etc/group` manually.
2. This command is part of the `GNU coreutils` package. For more info, see `man 1 id` or `info coreutils 'id invocation'`.
