groups
===

Print the names of the groups a specific user is in.

## Synopsis

```shell
groups [OPTION]... [username]...
```

## Description

- Prints the names of the groups that the specified user belongs to.

## Options

```shell
--help       # Display help information and exit.
--version    # Display version information and exit.
```

## Parameters

username (optional): One or more usernames. If not provided, the command defaults to the current user.

## Return Value

Returns 0 on success and a non-zero value on failure.

## Examples

Display the groups for the user `linux`:

```shell
[root@localhost ~]# groups linux
linux : linux adm dialout cdrom plugdev lpadmin admin sambashare
```

### Note

1. This command is equivalent to `id -Gn`.
2. Each user belongs to one group specified in `/etc/passwd` and potentially other groups specified in `/etc/group`.
3. This command is part of the `GNU coreutils` package. For more information, see `man -s 1 groups` or `info coreutils 'groups invocation'`.
