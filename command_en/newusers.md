newusers
===

Batch create or update user accounts

## Description

The **newusers command** is used to create or update multiple user accounts in a batch operation.

### Syntax

```shell
newusers [user_file]
```

### Parameters

User File: A text file containing user information. The format of each line must be the same as `/etc/passwd`.

### Examples

Add users in bulk using the `newusers` command:

The usage is straightforward: provide a file with lines formatted exactly like `/etc/passwd`.

```shell
username:password:UID:GID:gecos:home_directory:shell
```

Example lines in the file:

```shell
jingang0:x:520:520::/home/jingang0:/sbin/nologin
jingang1:x:521:521::/home/jingang1:/sbin/nologin
......
```

**Note on Shell Types:**

To see all available shells on the host, you can use the `chsh` command:

```shell
[root@localhost beinan]# chsh --list
/bin/sh
/bin/bash
/sbin/nologin
/bin/ksh
/bin/tcsh
/bin/csh
/bin/zsh
```

Except for `/sbin/nologin`, these shells allow system login. `/sbin/nologin` is typically used for virtual or service users who should not have shell access. If you want to add such a user, set their shell to `/sbin/nologin`, as shown in the example above.

For details on username, UID, GID, and home directory requirements, refer to relevant system documentation.
