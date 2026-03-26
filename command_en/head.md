head
===

Output the first part of files.

## Synopsis

```shell
head [OPTION]... [FILE]...
```

## Description

- Displays the first 10 lines of each file by default if no line count is specified.
- When processing multiple files, each file's output is preceded by a header showing the filename.
- If no file is specified, or if the file is `-`, the command reads from standard input.

## Options

```shell
-c, --bytes=[-]NUM       Output the first NUM bytes; with a leading "-", output all but the last NUM bytes of each file.
-n, --lines=[-]NUM       Output the first NUM lines instead of the default 10; with a leading "-", output all but the last NUM lines of each file.
-q, --quiet, --silent    Never print headers giving file names.
-v, --verbose            Always print headers giving file names.
-z, --zero-terminated    Line delimiter is NUL, not newline.
--help                   Display help information and exit.
--version                Display version information and exit.

NUM may have a multiplier suffix:
b 512
kB 1000
k 1024
MB 1000*1000
M 1024*1024
GB 1000*1000*1000
G 1024*1024*1024
T, P, E, Z, Y etc.

Binary prefixes can also be used:
KiB=K, MiB=M, and so on.
```

## Parameters

FILE (optional): One or more files to process.

## Return Value

Returns 0 on success and a non-zero value on failure.

## Examples

```shell
# View the first 6 lines of a history file:
[user2@pc ~]$ head -n 6 ~/.bash_history
#1575425555
cd ~
#1575425558
ls -lh
#1575425562
vi ~/Desktop/ZhuangZhu-74.txt
```

```shell
# View multiple files:
[user2@pc ~]$ head -n 5 ~/.bash_history ~/.bashrc
==> /allhome/user2/.bash_history <==
#1575425555
cd ~
#1575425558
ls -lh
#1575425562
vi ~/Desktop/ZhuangZhu-74.txt
#1575425566
uptime

==> /allhome/user2/.bashrc <==
# .bashrc

# forbid use Ctrl+D to exit shell.
set -o ignoreeof

# Source global definitions.
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi
```

### Note

1. This command is part of the `GNU coreutils` package. For more information, see `man -s 1 head` or `info coreutils 'head invocation'`.
    