lsof
===

List open files

## Description

The **lsof command** (list open files) is used to display a list of all open files and the processes that opened them. This includes regular files, directories, block special files, character special files, executing texts, shared libraries, and network files (TCP and UDP sockets). Because `lsof` needs to access kernel memory and various files, it typically requires root privileges to execute.

In Linux, everything is a file. Through files, you can access not only regular data but also network connections and hardware. For example, TCP and UDP sockets are assigned file descriptors by the system, providing a common interface for interaction between applications and the underlying operating system. Viewing the list of file descriptors opened by an application provides significant information about the application itself, which is helpful for system monitoring and troubleshooting.

### Syntax

```shell
lsof [OPTION]...
```

### Options

```shell
-a          List files that match all selection criteria (AND).
-c <cmd>    List files opened by processes starting with <cmd>.
-g          List process group IDs (PGID).
-d <fd>     List processes using the specified file descriptor.
+d <dir>    List open files in the specified directory.
+D <dir>    Recursively list open files in the specified directory.
-n          Inhibit the conversion of network numbers to host names.
-i <cond>   List files matching the specified network condition (protocol, port, @ip).
-p <pid>    List files opened by the specified process ID.
-u <user>   List files opened by the specified user (UID or name).
-h          Display help information.
-v          Display version information.
```

### Examples

```shell
lsof
COMMAND     PID USER   FD      TYPE             DEVICE     SIZE       NODE NAME
init          1 root  cwd       DIR                8,2     4096          2 /
init          1 root  rtd       DIR                8,2     4096          2 /
init          1 root  txt       REG                8,2    43496    6121706 /sbin/init
init          1 root  mem       REG                8,2   143600    7823908 /lib64/ld-2.5.so
init          1 root  mem       REG                8,2  1722304    7823915 /lib64/libc-2.5.so
init          1 root  mem       REG                8,2    23360    7823919 /lib64/libdl-2.5.so
init          1 root  mem       REG                8,2    95464    7824116 /lib64/libselinux.so.1
init          1 root  mem       REG                8,2   247496    7823947 /lib64/libsepol.so.1
init          1 root   10u     FIFO               0,17                1233 /dev/initctl
...
```

**Columns in lsof output:**

Column | Description
:- | :-
`COMMAND` | Name of the process
`PID` | Process ID
`PPID` | Parent process ID (requires -R)
`USER` | Owner of the process
`PGID` | Process group ID
`FD` | File descriptor

**File Descriptor (FD) values:**

Value | Description
:- | :-
`cwd`  | Current working directory
`txt`  | Program text (code, e.g., executable or shared library)
`lnn`  | Library reference (AIX)
`er`   | FD information error
`jld`  | Jail directory (FreeBSD)
`ltx`  | Shared library text
`mxx`  | Hex memory-mapped type number xx
`m86`  | DOS Merge mapped file
`mem`  | Memory-mapped file
`mmap` | Memory-mapped device
`pd`   | Parent directory
`rtd`  | Root directory
`tr`   | Kernel trace file (OpenBSD)
`v86`  | VP/ix mapped file
`0`    | Standard input (stdin)
`1`    | Standard output (stdout)
`2`    | Standard error (stderr)

**File status modes (following FD):**

Mode | Description
:- | :-
`u` | Open for read and write
`r` | Open for read-only
`w` | Open for write-only
` ` | Unknown status, not locked
`-` | Unknown status, locked

**Lock types (following status mode):**

Type | Description
:- | :-
`N`     | Solaris NFS lock of unknown type
`r`     | Read lock on part of the file
`R`     | Read lock on the entire file
`w`     | Write lock on part of the file
`W`     | Write lock on the entire file
`u`     | Read and write lock of any length
`U`     | Unknown lock type
`x`     | SCO OpenServer Xenix lock on part of the file
`X`     | SCO OpenServer Xenix lock on the entire file
`space` | No lock

**File types (TYPE column):**

Type | Description
:- | :-
`DIR` | Directory
`CHR` | Character special file
`BLK` | Block special file
`UNIX` | UNIX domain socket
`FIFO` | FIFO (First In First Out) pipe
`IPv4` | IPv4 socket
`IPv6` | IPv6 socket
`DEVICE` | Device name
`SIZE` | File size
`NODE` | Inode number
`NAME` | Name of the file
`REG` | Regular file

List files opened by a specific PID:

```shell
lsof -p $pid
```

Get PID for a specific listening port:

```shell
lsof -i:9981 -P -t -sTCP:LISTEN
```

List processes that have a specific file open:

```shell
lsof $filename
```

Check port usage:

```shell
lsof -i:$port
```

List all open files:

```shell
lsof
```

List files opened by a specific user:

```shell
lsof -u <username>
```

List network-related processes:

```shell
lsof -i
```

List processes using a specific directory:

```shell
lsof +D /path/to/directory
```

List files that have been deleted but are still open:

```shell
lsof -u +L1
```

List files open on a specific filesystem:

```shell
lsof /mountpoint
```

Inhibit host name lookup:

```shell
lsof -n
```
