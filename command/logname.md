logname
===

Print the name of the user currently logged into the terminal.

## Synopsis

```shell
logname [OPTION]...
```

## Main Purpose

- Print the name of the user currently logged into the terminal.

## Options

```shell
--help       Display help information and exit.
--version    Display version information and exit.
```

## Return Value

Returns 0 on success, and a non-zero value on failure.

## Examples

```shell
[root@localhost ~]# logname
root
```

### Notes

1. Note the difference between `whoami` and `logname`. For example, if you open a terminal as `root` and then switch to `user2` (e.g., using `su`), `whoami` will return `user2`, while `logname` will still return `root`. You can verify this in your own environment.

2. This command is part of the `GNU coreutils` package. For more information, refer to `man -s 1 logname` or `info coreutils 'logname invocation'`.
