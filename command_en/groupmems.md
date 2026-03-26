groupmems
===

Manage members of a user's primary group.

## Supplemental Information

The `groupmems` command allows a user to manage their own group membership list without requiring superuser privileges. The `groupmems` utility is intended for systems that configure users with a primary group in their own name (e.g., guest/guest).

Only a superuser acting as an administrator can use `groupmems` to change the membership of other groups.

### Syntax

```shell
groupmems -a user_name | -d user_name | [-g group_name] | -l | -p
```

### Options

```bash
-a, --add user_name    # Add a user to the group membership list. If the /etc/gshadow file exists and the group has no entry in it, a new entry will be created.

-d, --delete user_name # Remove a user from the group membership list.
                       # If /etc/gshadow exists, the user will be removed from both the members and administrators lists.
                       # If /etc/gshadow exists and the group has no entry, a new entry will be created.

-g, --group group_name # Allows the superuser to specify the group membership list to be modified.
-l, --list             # List the group membership list.
-p, --purge            # Clear all users from the group membership list.
                       # If /etc/gshadow exists and the group has no entry, a new entry will be created.
```

## Configuration

The following configuration variables in `/etc/login.defs` change the behavior of this tool:

```shell
MAX_MEMBERS_PER_GROUP (number)
```

Maximum members per group entry. When the maximum is reached, a new group entry (line) is started in `/etc/group` (with the same name, same password, and same GID).

The default value is 0, meaning there is no limit on the number of members in a group.

This feature (split groups) allows limiting the line length in the group file. This helps ensure that lines for NIS groups do not exceed 1024 characters.

If you need to enforce such a limit, you can use a value like 25.

Note: Not all tools support split groups (even within the Shadow tool suite). You should not use this variable unless you absolutely need it.

## Examples

The `groupmems` executable should be set to mode 2770 as user `root` and group `groups`. System administrators can add users to the `groups` group to allow or disallow them from using the `groupmems` utility to manage their own group membership lists.

```shell
groupadd -r groups
chmod 2770 groupmems

chown root.groups groupmems
groupmems -g groups -a gk4
```

Let's create a new user and a new group and verify the results:

```shell
useradd student
passwd student
groupadd staff
```

Make the user `student` a member of the `staff` group:

```shell
groupmems -g staff -a student
groupmems -g staff -l 
```

Add a user to a group:

```shell
groupmems -a mike -g SUPPORT
groupmems --add mike -g SUPPORT 
```

Delete/remove a user from a group:

```shell
groupmems -d mike -g SUPPORT
groupmems --delete mike -g SUPPORT
```

Change the group being managed:

```shell
groupmems -g SUPPORT
```

Purge all users from a group:

```shell
groupmems -p -g SUPPORT
groupmems --purge -g SUPPORT
```

List the members of a group:

```shell
groupmems -l -g SUPPORT
groupmems --list -g SUPPORT
```
