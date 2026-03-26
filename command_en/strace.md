strace
===

Trace system calls and signals

## Description

The **strace command** is a diagnostic, debugging, and instructional tool. It can be used to monitor and analyze the system calls and signal deliveries of an application to resolve issues or understand how the application works. While `strace` is not a professional debugger like `gdb`, it is highly effective for observing process-kernel interactions.

The simplest usage of `strace` is to execute a specified command, and it exits once the command completes. During execution, `strace` records and parses all system calls made by the process and all signals received by the process.

### Syntax

```shell
strace  [  -dffhiqrtttTvxx  ] [ -acolumn ] [ -eexpr ] ...
    [ -ofile ] [-ppid ] ...  [ -sstrsize ] [ -uusername ]
    [ -Evar=val ] ...  [ -Evar  ]...
     [command [ arg ...  ] ]

strace  -c  [ -eexpr ] ...  [ -Ooverhead ] [ -Ssortby ]
    [ command [ arg...  ] ]
```

### Options

```shell
-c: Count time, calls, and errors for each system call.
-d: Output strace debugging information to standard error.
-f: Trace child processes created by fork.
-ff: If -o filename is provided, output trace results for each process to filename.pid.
-F: Attempt to trace vfork calls (with -f, vfork is normally not traced).
-h: Output brief help information.
-i: Output the entry point pointer of the system call.
-q: Suppress messages about detaching.
-r: Print a relative timestamp for each system call.
-t: Prefix each line with the time of day.
-tt: Prefix each line with the time of day, including microseconds.
-ttt: Output timestamps in seconds and microseconds.
-T: Show the time spent in each system call.
-v: Output all system calls. Some calls regarding environment variables, status, I/O, etc., are omitted by default due to high frequency.
-V: Output strace version information.
-x: Output non-standard strings in hexadecimal format.
-xx: Output all strings in hexadecimal format.
-a column: Set the alignment for return values (default is 40).
-e expr: Specify an expression to control tracing. Format: [qualifier=][!]value1[,value2]...
         Qualifiers: trace, abbrev, verbose, raw, signal, read, write. Default is trace.
         Example: -e open is equivalent to -e trace=open. -e trace!=open traces all calls except open.
         Special symbols: all and none. (Note: use \! to escape ! in some shells).
-e trace=set: Trace only the specified set of system calls. e.g., -e trace=open,close,read,write.
-e trace=file: Trace system calls related to file operations.
-e trace=process: Trace system calls related to process control.
-e trace=network: Trace system calls related to networking.
-e trace=signal: Trace system calls related to signals.
-e trace=ipc: Trace system calls related to IPC.
-e abbrev=set: Set the set of system calls to abbreviate. -v is equivalent to abbrev=none.
-e raw=set: Display arguments of the specified system calls in hexadecimal.
-e signal=set: Specify the signals to trace (default is all). e.g., signal=!SIGIO.
-e read=set: Output data read from the specified file descriptors. e.g., -e read=3,5.
-e write=set: Output data written to the specified file descriptors.
-o filename: Write output to the specified file.
-p pid: Trace the process with the specified PID.
-s strsize: Specify the maximum length of strings to output (default is 32). File names are always output in full.
-u username: Run the command to be traced with the UID and GID of the specified user.
```

### Examples

**Tracing System Calls**

Here is a simple program to demonstrate the basic usage of `strace`. The C code is as follows:

```shell
# filename test.c
#include <stdio.h>

int main()
{
    int a;
    scanf("%d", &a);
    printf("%09d\n", a);
    return 0;
}
```

Compile it with `gcc -o test test.c` and run it with `strace`:

```shell
strace ./test
```

During execution, it will wait for an integer input. If you input 99, you get:

```shell
// Result of running test directly
oracle@orainst[orcl]:~ $./test
99
000000099

// Result of running test via strace
oracle@orainst[orcl]:~ $strace ./test

// strace output
execve("./test", ["./test"], [/* 41 vars */]) = 0
uname({sys="Linux", node="orainst.desktop.mycompany.com", ...}) = 0
brk(0)                                  = 0x8078000
fstat64(3, {st_mode=S_IFREG|0644, st_size=65900, ...}) = 0
old_mmap(NULL, 65900, PROT_READ, MAP_PRIVATE, 3, 0) = 0xbf5ef000
close(3)                                = 0
open("/lib/tls/libc.so.6", O_RDONLY)    = 3
read(3, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\3\0\3\0\1\0\0\0\200X\1"..., 512) = 512
fstat64(3, {st_mode=S_IFREG|0755, st_size=1571692, ...}) = 0
old_mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xbf5ee000
old_mmap(NULL, 1275340, PROT_READ|PROT_EXEC, MAP_PRIVATE, 3, 0) = 0xa02000
old_mmap(0xb34000, 12288, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED, 3, 0x132000) = 0xb34000
old_mmap(0xb37000, 9676, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0xb37000
close(3)                                = 0
set_thread_area({entry_number:-1 -> 6, base_addr:0xbf5ee740, limit:1048575, seg_32bit:1, contents:0, read_exec_only:0, limit_in_pages:1, seg_not_present:0, useable:1}) = 0
munmap(0xbf5ef000, 65900)               = 0
fstat64(0, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xbf5ff000
read(0, 99
"99\n", 1024)                   = 3
fstat64(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xbf5fe000
write(1, "000000099\n", 10)             = 10
munmap(0xbf5fe000, 4096)                = 0
exit_group(0)                           = ?
```

As seen in the output, the system first calls `execve` to start a new process, then initializes the environment, and finally pauses at `read(0, ...)` waiting for input (our `scanf`). After inputting 99, `write` is called to output "000000099" to the screen, and finally `exit_group` is called to terminate the process.

**Tracing Signal Delivery**

Using the same `test` program, run `strace ./test` and wait at the input prompt. In another terminal, run:

```shell
killall test
```

The output in the first terminal will show:

```shell
read(0, 0xbf5ff000, 1024)               = ? ERESTARTSYS (To be restarted)
--- SIGTERM (Terminated) @ 0 (0) ---
+++ killed by SIGTERM +++
```

It clearly shows that the process was "+++ killed by SIGTERM +++".

**System Call Statistics**

Using the `-c` flag, `strace` can provide a statistical analysis of all system calls:

```shell
strace -c ./test
```

Example output:

```shell
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 45.90    0.000140           5        27        25 open
 34.43    0.000105           4        24        21 stat64
  7.54    0.000023           5         5           old_mmap
  2.62    0.000008           8         1           munmap
  1.97    0.000006           6         1           uname
  1.97    0.000006           2         3           fstat64
  1.64    0.000005           3         2         1 read
  1.31    0.000004           2         2           close
  0.98    0.000003           3         1           brk
  0.98    0.000003           3         1           mmap2
  0.66    0.000002           2         1           set_thread_area
------ ----------- ----------- --------- --------- ----------------
100.00    0.000305                    68        47 total
```

This lists which system functions were called, how many times, and how much time they consumed.

### Common Parameters

**Redirecting Output**

The `-o` parameter writes the output to a file. Without it, output goes to `STDERR`.

```shell
strace -c -o test.txt ./test
strace -c ./test 2>test.txt
```

**Timing System Calls**

The `-T` parameter prints the time spent in each system call at the end of the line.

```shell
strace -T ./test

read(0, "1\n", 1024)                    = 2 <2.673455>
write(1, "000000001\n", 10)             = 10 <0.000016>
```

**Timestamps**

Flags like `-t`, `-tt`, and `-ttt` record when each system call occurred.

| Parameter | Example Output | Description |
| --- | --- | --- |
| -t | 10:33:04 exit_group(0) | Precise to seconds |
| -tt | 10:33:48.159682 exit_group(0) | Precise to microseconds |
| -ttt | 1262169244.788478 exit_group(0) | Unix timestamp with microsecond precision |

**Truncating Output**

The `-s` parameter specifies the maximum string length to output for each line.

```shell
strace -s 20 ./test
```

**Tracing an Existing Process**

Use `-p` followed by the PID to trace a running process.

```shell
strace -p pid
```

### Comprehensive Example: Monitoring Oracle lgwr Process

To investigate whether Oracle's `lgwr` process writes to log files every 3 seconds as documented:

1. Get the PID of `lgwr`:
   `ps -ef | grep lgwr` (e.g., PID 5912)

2. Start `strace`:
   `strace -tt -s 10 -o lgwr.txt -p 5912`

3. Analyze the results, looking for `pwrite` calls:
   `grep "pwrite(2" lgwr.txt` (assuming file handles starting with 2 relate to log files).

This allows you to verify the actual behavior of the process against the documentation.
