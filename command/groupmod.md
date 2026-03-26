groupmod
===

Modify a group definition on the system.

## Supplemental Information

The **groupmod command** modifies the definition of a specified group by altering the appropriate entries in the group databases (`/etc/group` and `/etc/gshadow`). This includes changing the GID, group members, group name, group password, etc.

### Syntax

```shell
groupmod (options) (parameters)
```

### Options

```shell
-a, --append: Used with the -U option to append specified users to the existing member list instead of overwriting.
-g, --gid GID: Modify the GID of the group to the specified value. It must be a non-negative, unique integer (unless the -o option is used). Members using this group as their primary group will be updated automatically.
-n, --new-name NEW_GROUP_NAME: Set the new name for the group.
-o: Allow setting a duplicate GID.
-p, --password PASSWORD: Set the group password (alternatively, modify /etc/gshadow directly). The password must be encrypted using crypt. This allows non-members to temporarily switch to the group using newgrp, though this mechanism is not recommended in modern systems.
-U, --users user1,user2...: A comma-separated list of users to replace the current group members; if -a is also specified, users are appended to the existing list.
```

### Parameters

Group Name: Specifies the group to be modified.

### Examples

Modify the GID of `group1`:

```shell
groupmod -g 1003 group1
```

Modify the GID of `group2` to a duplicate GID `1003`:

```shell
groupmod -g 1003 -o group2
```

Rename `group2` to `group3`:

```shell
groupmod -n group3 group2
```

Overwrite members of `group3` with `user1`:

```shell
groupmod -U user1 group3
```

Append `user2` and `user3` to `group3`:

```shell
groupmod -a -U user2,user3 group3
```

### Note

On some systems (like Ubuntu 22.04), the `groupmod` command may not support the `-a` and `-U` options. You can use the `gpasswd` command instead.

```shell
groupmod -U user1,user2 groupname
```

is equivalent to:

```shell
gpasswd -M "" groupname
gpasswd -M user1,user2 groupname
```

and

```shell
groupmod -a -U user1,user2,user3 groupname
```

is equivalent to:

```shell
gpasswd -a user1 groupname
gpasswd -a user2 groupname
gpasswd -a user3 groupname
```
