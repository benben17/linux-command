users
===

Print the user names of users currently logged in to the current host.

## Synopsis

```shell
users [OPTION]... [FILE]
```

## Main Uses

- Each displayed username corresponds to a login session; if a user has more than one login session, their username will be displayed the same number of times.

## Options

```shell
--help       Display help information and exit.
--version    Display version information and exit.
```

## Parameters

FILE (optional): The file that records current user logins; defaults to `/var/run/utmp` and `/var/log/wtmp`.

## Return Value

Returns 0 on success, and a non-zero value on failure.

## Examples

```shell
[root@localhost ~]# users
root root
```

### Note

1. This command is part of the `GNU coreutils` package. For related help information, please see `man -s 1 users` or `info coreutils 'users invocation'`.
