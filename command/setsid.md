setsid
===

Run a program in a new session.

## Description

The **setsid command** allows a child process to break away from its parent process's Session ID, Process Group ID, and controlling terminal. While this can be achieved in code by calling the `setsid` function, the `setsid` command provides a way to do this from the command line or within scripts. It helps a process detach from the inherited terminal, process group, and session of its parent.

### Syntax

```shell
setsid [options] <program> [arguments ...]
```

### Options

```shell
-c, --ctty   Set the controlling terminal to the current one.
-f, --fork   Always fork.
-w, --wait   Wait for the program to exit and return its exit status.
```

### Examples

Using `setsid` is very straightforward; simply prefix the command you want to run with `setsid`:

```shell
[root@root ~]# setsid ping www.ibm.com
[root@root ~]# ps -ef | grep www.ibm.com
root 31094 1 0 07:28 ? 00:00:00 ping www.ibm.com
root 31102 29217 0 07:29 pts/4 00:00:00 grep www.ibm.com
[root@root ~]#
```
