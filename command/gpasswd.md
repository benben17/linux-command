gpasswd
===

A tool for managing group files in Linux.

## Supplemental Information

The **gpasswd command** is a management tool for the group files `/etc/group` and `/etc/gshadow` in Linux.

### Syntax

```shell
gpasswd (options) (parameters)
```

### Options

```shell
-a: Add a user to the group;
-d: Remove a user from the group;
-A: Assign group administrators;
-M: Assign group members (similar to -A);
-r: Remove the group password;
-R: Restrict access to the group (only members can use newgrp).
```

### Parameters

Group: Specifies the group to manage.

### Examples

If there is an account `peter` who is not a member of `groupname`, they would typically need a password to use `newgrp`.

```shell
gpasswd groupname
```

To let a user temporarily join a group (so files created by `peter` will belong to `groupname`):

```shell
gpasswd -A peter users
```

Now `peter` is an administrator of the `users` group and can perform the following:

```shell
gpasswd -a mary users
gpasswd -a allen users
```

Note: To add a user to a group while keeping their existing group memberships, use `gpasswd -a`:

```shell
gpasswd -a user_name group_name
```
