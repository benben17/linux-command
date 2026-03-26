ltrace
===

A library call tracer

## Description

The **ltrace command** is used to intercept and record the dynamic library calls which are called by the executed process and the signals which are received by that process. It can also intercept system calls made by the program.

### Syntax

```shell
ltrace [OPTION]... [COMMAND [ARG...]]
```

### Options

```shell
-a <column>     Align return values in a specific column.
-c              Count time and calls and report a summary on program exit.
-C, --demangle  Decode (demangle) low-level symbol names into user-level names.
-d              Print debugging information.
-e <expr>       A qualifying expression which modifies which library calls to trace.
-f              Trace child processes as they are created by currently traced processes.
-h, --help      Display help and exit.
-i              Print the instruction pointer at the time of the library call.
-l <library>    Trace only calls to functions implemented in the specified library.
-L              Do not display library calls (use with -S to see only system calls).
-n, --indent <nr> Indent output by <nr> spaces for each level of call nesting.
-o, --output <file> Write the trace output to the specified file.
-p <pid>        Attach to the process with the specified PID.
-r              Print a relative timestamp of each line of the trace.
-s <strlen>     Specify the maximum string size to print.
-S              Trace system calls as well as library calls.
-t, -tt, -ttt   Print absolute timestamps.
-T              Show the time spent inside each call.
-u <username>   Run the command with the specified user ID or group ID.
-V, --version   Display version information and exit.
-x <name>       Treat the global symbol <name> as a library subroutine.
```

### Examples

Basic usage without parameters:

```shell
[guest@localhost tmp]$ ltrace ./a.out
__libc_start_main(0x80484aa, 1, 0xbfc07744, 0x8048550, 0x8048540 <unfinished ...>
printf("no1:%d \t no2:%d \t diff:%d\n", 10, 6, 4no1:10 no2:6 diff:4 ) = 24
printf("no1:%d \t no2:%d \t diff:%d\n", 9, 7, 2no1:9 no2:7 diff:2 ) = 23
printf("no1:%d \t no2:%d \t diff:%d\n", 8, 8, 0no1:8 no2:8 diff:0 ) = 23
--- SIGFPE (Floating point exception) ---
+++ killed by SIGFPE +++
```

Show time spent in each call:

```shell
[guest@localhost tmp]$ ltrace -T ./a.out
__libc_start_main(0x80484aa, 1, 0xbf81d394, 0x8048550, 0x8048540 <unfinished ...>
printf("no1:%d \t no2:%d \t diff:%d\n", 10, 6, 4no1:10 no2:6 diff:4 ) = 24 <0.000972>
printf("no1:%d \t no2:%d \t diff:%d\n", 9, 7, 2no1:9 no2:7 diff:2 ) = 23 <0.000155>
printf("no1:%d \t no2:%d \t diff:%d\n", 8, 8, 0no1:8 no2:8 diff:0 ) = 23 <0.000153>
--- SIGFPE (Floating point exception) ---
+++ killed by SIGFPE +++
```

Trace system calls:

```shell
[guest@localhost tmp]$ ltrace -S ./a.out
SYS_brk(NULL) = 0x9e20000
SYS_access(0xa4710f, 4, 0xa4afc0, 0, 0xa4b644) = 0
SYS_open("/etc/ld.so.preload", 0, 02) = 3
SYS_fstat64(3, 0xbfbd7a94, 0xa4afc0, -1, 3) = 0
SYS_mmap2(0, 17, 3, 2, 3) = 0xb7f2a000
SYS_close(3) = 0
SYS_open("/lib/libcwait.so", 0, 00) = 3
SYS_read(3, "\177ELF\001\001\001", 512) = 512
SYS_fstat64(3, 0xbfbd76fc, 0xa4afc0, 4, 0xa4b658) = 0
SYS_mmap2(0, 4096, 3, 34, -1) = 0xb7f29000
SYS_mmap2(0, 5544, 5, 2050, 3) = 0x423000
SYS_mmap2(0x424000, 4096, 3, 2066, 3) = 0x424000
...
```
