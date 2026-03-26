who
===

Display who is logged in

## Synopsis

```shell
who [OPTION]... [file] [am i]
```

## Description

- When no non-option arguments are provided, `who` prints information about each current user in the following order: username, terminal info, login time, and remote host or X display.
- When the user executes `who am i`, it displays only information about the user running the command.

## Options

```shell
-a, --all                                Same as '-b -d --login -p -r -t -T -u'.
-b, --boot                               Time of last system boot.
-d, --dead                               Print dead processes.
-H, --heading                            Print column headings.
-l, --login                              Print system login processes.
--lookup                                 Attempt to canonicalize hostnames via DNS.
-m                                       Only show hostname and user associated with stdin.
-p, --process                            Print active processes spawned by init.
-q, --count                              List all login names and number of users logged in.
-r, --runlevel                           Print current runlevel.
-s, --short                              Only print name, line, and time (default).
-t, --time                               Print last system clock change.
-T, -w, --mesg, --message, --writable    Add one of '+, -, ?' as a user message status after the username.
-u, --users                              List users logged in.
--help                                   Display help and exit.
--version                                Display version and exit.

About message status (+, -, ?):
'+'  Allow writing messages (mesg y)
'-'  Disallow writing messages (mesg n)
'?'  Cannot find terminal device
```

## Parameters

file (optional): Specify a file instead of the default `/var/run/utmp` or `/etc/utmp`. Typically `/var/log/wtmp` is used to see past logins.

## Return Value

Returns 0 on success and non-zero on failure.

## Examples

```shell
[root@localhost ~]# who
root     pts/0        2013-08-19 15:04 (192.168.0.134)
root     pts/1        2013-12-20 10:37 (180.111.155.40)

[root@localhost ~]# who -q
root root
# users=2

[root@localhost ~]# who -H
NAME     LINE         time             COMMENT
root     pts/0        2013-08-19 15:04 (192.168.0.134)
root     pts/1        2013-12-20 10:37 (180.111.155.40)

[root@localhost ~]# who -w
root     + pts/0        2013-08-19 15:04 (192.168.0.134)
root     + pts/1        2013-12-20 10:37 (180.111.155.40)
```

### Note

1. This command is part of the `GNU coreutils` package. For more help, see `man -s 1 who`.
