arch
===

Display the hardware architecture type of the current host

## Summary

```shell
arch [OPTION]...
```

## Main Purpose

- Print machine architecture information; output of the `arch` command includes: i386, i486, i586, alpha, sparc, arm, m68k, mips, ppc, i686, etc.

## Options

```shell
--help       Display help information and exit.
--version    Display version information and exit.
```

## Examples

```shell
[root@localhost ~]# arch
x86_64
```

### Note

1. This command is equivalent to `uname -m`.

2. This command is part of the `GNU coreutils` package. For related help information, please refer to `man -s 1 arch` or `info coreutils 'arch invocation'`.
