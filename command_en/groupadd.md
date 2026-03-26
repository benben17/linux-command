groupadd
===

Create a new group.

## Supplemental Information

The **groupadd command** is used to create a new group. The information for the new group will be added to the system files.

### Syntax

```shell
groupadd (options) (parameters)
```

### Options

```shell
-g: Specify the numerical value of the group's ID (GID);
-r: Create a system group (typically with a GID less than 500 or 1000, depending on the system);
-K: Overwrite configuration defaults from /etc/login.defs;
-o: Allow the creation of a group with a non-unique GID.
```

### Parameters

Group Name: The name of the group to be created.

### Examples

Create a new group with a specific group ID:

```shell
groupadd -g 344 jsdigname
```

This will create an entry in the `/etc/group` file with a GID of 344.
