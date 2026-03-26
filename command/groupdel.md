groupdel
===

Delete a specific group.

## Supplemental Information

The **groupdel command** is used to remove an existing group from the system. This command modifies the `/etc/group` and `/etc/gshadow` files. If the group is the primary group of any user, that user must be deleted or have their primary group changed before the group can be deleted. If the group is only a secondary group for some users, it can be deleted directly, and the group information will be removed for those users.

### Syntax

```shell
groupdel (parameters)
```

### Parameters

Group: The name of the group to be deleted.

### Examples

```shell
groupadd damon  # Create the 'damon' group
groupdel damon  # Delete the 'damon' group
```
