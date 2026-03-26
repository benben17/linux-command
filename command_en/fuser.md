fuser
===

Identify processes using files or sockets.

## Description

The **fuser command** is used to report which processes are using specific files or network sockets. It lists the Process IDs (PIDs) of local processes that are using the files specified by the `file` parameter. For block special devices, it lists processes using any file on that device.

Each PID is followed by a letter indicating the type of access:

* `c`: Current directory.
* `e`: Executable being run.
* `f`: Open file (not shown by default).
* `F`: Open file for writing (not shown by default).
* `r`: Root directory.
* `m`: Memory-mapped file or shared library.

### Syntax

```shell
fuser (options) (parameters)
```

### Options

```shell
-a: Display all files specified on the command line.
-k: Kill all processes accessing the specified files.
-i: Ask for user confirmation before killing a process.
-l: List all known signal names.
-m: Specify a mounted filesystem or a mounted block device.
-n: Select a different name space (file, tcp, or udp).
-u: Display the user name of the process owner after each PID.
```

### Parameters

File: Can be a filename or a TCP/UDP port number.

### Examples

To list the PIDs of local processes using the `/etc/passwd` file:

```shell
fuser /etc/passwd
```

To list the PIDs and usernames of processes using the `/etc/filesystems` file:

```shell
fuser -u /etc/filesystems
```

To terminate all processes using a given filesystem:

```shell
fuser -k -x -u -c /dev/hd1  # OR
fuser -kxuc /home
```

Either command lists the PIDs and usernames and then terminates every process using the `/dev/hd1` (or `/home`) filesystem. Only the root user can terminate processes belonging to another user. This command is useful if you are trying to unmount a filesystem that is currently busy.

To list all processes using files that have been deleted from a given filesystem:

```shell
fuser -d /usr
```

Note: `/dev/kmem` and `/dev/mem` are used for system images.
