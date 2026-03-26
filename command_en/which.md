which
===

Locate a command and display its absolute path

## Description

The **which command** is used to find and display the absolute path of a given command. It searches for executable files in the directories specified by the `PATH` environment variable. By using `which`, you can check if a certain system command exists and exactly which file will be executed when you type the command.

### Syntax

```shell
which [options] [command]
```

### Options

```shell
-a  Print all matching executables in PATH, not just the first one.
-n <length>  Specify the minimum filename length.
-p <length>  Same as -n, but includes the path.
-w  Specify the width of the output columns.
-V  Display version information.
```

### Parameters

command: A list of command names to locate.

### Examples

Find the path of a command:

```shell
[root@localhost ~]# which pwd
/bin/pwd

[root@localhost ~]# which adduser
/usr/sbin/adduser
```

Note: `which` searches based on the `PATH` variable. Different `PATH` settings will yield different results.

Try to find `cd`:

```shell
[root@localhost ~]# which cd
cd: shell built-in command
```

In some systems, `which` might not find `cd` because it's a shell builtin and not a standalone executable file in `PATH`.
