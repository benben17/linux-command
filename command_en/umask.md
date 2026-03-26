umask
===

Display or set the file mode creation mask.

## Synopsis

```shell
umask [-p] [-S] [mode]
```

## Main Purpose

- Display the current file mode creation mask.
- Set the file mode creation mask using an octal number.
- Set the file mode creation mask using symbolic notation.

## Parameters

mode (optional): Octal number or symbolic notation.

## Options

```shell
-p: When no parameters are provided, specifies that the output format should be reusable as input.
-S: Output the creation mask in symbolic notation; otherwise, it is output in octal.
```

## Return Value

Returns success unless an invalid option or parameter is provided.

## Examples

*The following examples assume a file mode creation mask of 0022.*

```shell
# Output the creation mask in octal format.
umask -p
# Result:
umask 0022
# Output the creation mask in symbolic notation.
umask -S
# Result:
u=rwx,g=rx,o=rx
```

> Referring to the `DESCRIPTION` section of `man chmod`:
> - `u` represents the current user.
> - `g` represents users in the same group as the current user (group users).
> - `o` represents other users.
> - `a` represents all users.
> - `r` represents read permission (octal 4).
> - `w` represents write permission (octal 2).
> - `x` represents execute permission (octal 1).
> - `+` adds the specified permissions to the target user(s).
> - `-` removes the specified permissions from the target user(s).
> - `=` adds the specified permissions and removes those not mentioned.

The symbolic output `u=rwx,g=rx,o=rx` translates to octal `0755`.

To set the same permissions using an octal mask, `umask` requires the subtraction `0777 - 0755`, which equals `0022` (whereas `chmod` does not).

Adding, removing, and assigning permissions in symbolic mode:

```shell
# Add permission:
# Add write permission for group users.
umask g+w
# Remove permission:
# Remove write and execute permissions for other users.
umask o-wx
# Assign permission:
# Assign all permissions to all users (equivalent to umask u=rwx,g=rwx,o=rwx).
umask a=rwx
# Clear all permissions for other users.
umask o=
```

Creating directories and files (assuming they don't exist in the current directory):

```shell
# Create a file
touch test.sh
# Check permissions; note that execute permission settings do not apply to files by default.
stat test.sh
# Create a directory
mkdir newdir
# Check permissions; execute permission settings do apply to directories.
stat newdir
```

### Notes

1. This command is a bash built-in; see the `help` command for related help information.
2. `chmod` is used to change the permissions of existing objects, while `umask` affects the permissions of newly created objects.
3. **Use this command with caution.** Specifically, do not remove read permission for the current user, as it will cause errors when using the `TAB` key for completion in the terminal.
