tty
===

Print the filename of the terminal connected to standard input

## Synopsis

```shell
tty [option] ...
```

## Main Purpose

- Print the filename of the terminal connected to standard input. Prints "not a tty" if standard input is not a terminal.

## Options

```shell
-s, --silent, --quiet    Do not print anything, only return the exit status.
--help                   Display help information and exit.
--version                Display version information and exit.
```

## Return Value

When using `-s, --silent, --quiet`, a return code of 0 indicates standard input is a terminal, 1 indicates it is not, 2 indicates an option error, and 3 indicates a write error occurred.

## Example

Display the terminal device filename connected to current standard input.

```shell
[root@localhost ~]# tty
/dev/pts/2
```

Find the processes associated with the terminal (assuming it's pts/2):

```shell
# Note the filtering for the TTY column.
ps -ef | egrep "pts/2 " | grep -v grep
```

### Notes

1. This command is part of the `GNU coreutils` package. For more help, see `man -s 1 tty` or `info coreutils 'tty invocation'`.
