ulimit
===

Control shell resources

## Description

The **ulimit command** is used to limit system users' access to shell resources. If you're unsure what this means, the following explanation may help:

Consider a scenario where 10 users are logged into a Linux host simultaneously. Without system resource limits, if these 10 users each open 500 documents, and each document is 10 MB, the system's memory resources would face a massive challenge.

Actual application environments are often much more complex. For instance, in an embedded development environment, resources are extremely tight. There are strict requirements for the number of open file descriptors, stack size allocation, CPU time, virtual memory size, and more. Rational resource limitation and allocation are not only necessary for system availability but also closely linked to the performance of software running on the system. In such cases, `ulimit` plays a significant role as a simple and effective way to implement resource limits.

`ulimit` is used to limit the resources used by processes started by the shell, supporting various types of limits: core file size, process data segment size, shell process file creation size, locked-in-memory size, resident set size, number of open file descriptors, maximum stack size, CPU time, maximum number of threads per user, and maximum virtual memory used by the shell process. It supports both hard and soft resource limits.

As a temporary limit, `ulimit` acts on the shell session through which its command was used; the limit ends when the session terminates and does not affect other shell sessions. For permanent limits, `ulimit` command statements can be added to files read by the login shell to apply to specific shell users.

### Syntax

```shell
ulimit [options]
```

### Options

```shell
-a: Display current resource limit settings;
-c <core file limit>: Set the maximum size of core files, in blocks;
-d <data segment size>: Maximum size of the program's data segment, in KB;
-e: Default process priority; smaller values indicate higher priority;
-f <file size>: Maximum file size the shell can create, in blocks;
-H: Set hard resource limits (limits set by the administrator);
-m <memory size>: Set the maximum physical memory usage, in KB;
-n <number of files>: Set the maximum number of files that can be open simultaneously;
-p <buffer size>: Set the pipe buffer size, in 512-byte units;
-s <stack size>: Set the maximum stack size, in KB;
-S: Set soft resource limits;
-t <CPU time>: Set the maximum CPU usage time, in seconds;
-u <number of processes>: Set the maximum number of processes (including threads) the user can open;
-v <virtual memory size>: Set the maximum virtual memory usage, in KB.
```

### Example

```shell
[root@localhost ~]# ulimit -a
core file size          (blocks, -c) 0           # Max core file size is 0 blocks.
data seg size           (kbytes, -d) unlimited   # Process data segment can be any size.
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited   # Files can be any size.
pending signals                 (-i) 98304       # Max 98304 pending signals.
max locked memory       (kbytes, -l) 32          # Max physical memory a task can lock is 32 KB.
max memory size         (kbytes, -m) unlimited   # Max resident set size for a task.
open files                      (-n) 1024        # A task can open up to 1024 files simultaneously.
pipe size            (512 bytes, -p) 8           # Max pipe space is 4096 bytes (8 * 512).
POSIX message queues     (bytes, -q) 819200      # Max POSIX message queue size is 819200 bytes.
real-time priority              (-r) 0
stack size              (kbytes, -s) 10240       # Max stack size for a process is 10240 KB.
cpu time               (seconds, -t) unlimited   # CPU time used by the process.
max user processes              (-u) 98304       # Max concurrent processes (including threads) for the current user is 98304.
virtual memory          (kbytes, -v) unlimited   # No limit on the process's maximum address space.
file locks                      (-x) unlimited   # No limit on the maximum number of file locks.
```
