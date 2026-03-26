hostid
===

Display the hexadecimal identifier for the current host.

## Synopsis

```shell
hostid [OPTION]...
```

## Description

- Displays the unique hexadecimal identifier of the current host.
- Often used to limit software licensing or permissions; this ID is typically constant.

## Options

```shell
--help       # Display help information and exit.
--version    # Display version information and exit.
```

## Examples

```shell
[root@localhost ~]# hostid
007f0100
```

### Note

1. This command is part of the `GNU coreutils` package. For more information, see `man -s 1 hostid` or `info coreutils 'hostid invocation'`.
