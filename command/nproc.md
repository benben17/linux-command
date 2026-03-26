nproc
===

Print the number of processing units available

## Synopsis

```shell
nproc [OPTION]...
```

## Description

- Print the number of processing units available to the current process.

## Options

```shell
--all         Print the number of installed processors.
--ignore=N    If possible, exclude N processing units.
--help        Display help message and exit.
--version     Display version information and exit.
```

## Example

```shell
[root@localhost ~]# nproc
8
```

### Notes

1. This command is part of the `GNU coreutils` package. For more information, see `man -s 1 nproc` or `info coreutils 'nproc invocation'`.
