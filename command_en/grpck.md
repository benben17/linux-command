grpck
===

Verify the integrity of group files.

## Supplemental Information

The **grpck command** is used to verify the integrity of group files. Before verification, the group files `/etc/group` and `/etc/gshadow` are locked.

`grpck` checks if the data is correctly stored, if each record contains sufficient information, if there is a unique group name, if it contains valid users, and if group administrators are correctly set. If `grpck` detects an error, it prompts the user to delete the erroneous record. If the user does not explicitly choose to delete the record, `grpck` terminates.

### Syntax

```shell
grpck (options)
```

### Options

```shell
-r: Read-only mode;
-s: Sort entries by group ID.
```

### Examples

Verify the group and shadow files:

```shell
grpck   # Must be run as root
grpck /etc/group /etc/gshadow   # The two forms are equivalent; no output indicates no errors.
```

Example of testing an error:

```shell
# Add an incorrectly formatted line
echo check_user:x: >> /etc/group
cat /etc/group | grep check_user
# check_user:x:  (The GID field is empty, which is an error.)

grpck /etc/group 
# invalid group file entry
# delete line 'check_user:x:'? y      # Prompt to delete
# grpck: the files have been updated  # The erroneous line has been deleted.

cat /etc/group | grep check_user   # No result found, it has been deleted.
```
