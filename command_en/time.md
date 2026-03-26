time
===

Calculate the total time spent by a given command

## Description

The `time` command is used to determine how long a given command takes to run. It is useful for testing the performance of your scripts and commands.

For example, if you have two different scripts doing the same job and you want to know which one performs better, you can use the Linux time command to determine the execution time of each script.

This instruction covers both the shell built-in command and the standalone package. **Information about the standalone package is at the bottom of this document.**

## Syntax

```shell
time <command>
```

## Parameters

Command: Specifies the command and its parameters to be run.

## Examples

Execution time is crucial when testing a program or comparing different algorithms; a good algorithm should take the least time. All UNIX-like systems include the `time` command to calculate time consumption. For example:

```shell
$ time ls
anaconda-ks.cfg  install.log  install.log.syslog  satools  text

real    0m0.009s
user    0m0.002s
sys     0m0.007s
```

The output format may vary depending on the distribution or shell:

```shell
# Bash
real 0m33.961s
user 0m0.340s
sys 0m0.940s

# Zsh
0.34s user 0.94s system 4% cpu 33.961 total

# GNU time (sh)
0.34user 0.94system 0:33.96elapsed 4%CPU (0avgtext+0avgdata 6060maxresident)k
0inputs+201456outputs (0major+315minor)pagefaults 0swaps
```

`real`, `total`, or `elapsed` (wall clock time) refers to the time from the start of the call to its end. It is the time from the moment you press Enter until the command completes.
`user` - CPU time spent in user mode.
`system` or `sys` - CPU time spent in kernel mode.

## Package

The following section is about the `/usr/bin/time` binary executable provided by the `time` package, rather than the shell built-in `time` command.

### Package Syntax

Some shells (such as `bash`) have a built-in `time` command that provides similar information about time and potentially other resource usage.

To access the actual command, you may need to specify its path (e.g., `/usr/bin/time`).

```shell
time [options] command [arguments...]
```

### Package Options

-f format, --format=format
    Specify the output format, potentially overriding the format specified in the TIME environment variable.
-p, --portability
    Use the portable output format.
-o file, --output=file
    Do not send results to stderr, but overwrite the specified file instead.
-a, --append
    (Used with -o) Append instead of overwrite.
-v, --verbose
    Provide very detailed output about all information the program knows.
-q, --quiet
    Do not report abnormal program termination (when the command is terminated by a signal) or non-zero exit status.

### Package Examples

Use the `-o` option to write execution time to a file:

```shell
/usr/bin/time -o outfile.txt ls
```

Use the `-a` option to append information:

```shell
/usr/bin/time -a -o outfile.txt ls
```

Use the `-f` option to format the time output:

```shell
/usr/bin/time -f "time: %U" ls
```

Parameters for the `-f` option:

Parameter | Description
--- | ---
`%E` | Real time, format: [hours:]minutes:seconds
`%U` | User time.
`%S` | Sys time.
`%C` | Command name and command-line arguments.
`%D` | Process's non-shared data area, in KB.
`%x` | Command exit status.
`%k` | Number of signals received by the process.
`%w` | Number of times the process was swapped out of main memory.
`%Z` | System page size (a system constant, varies by system).
`%P` | Percentage of CPU time obtained by the process, equals `(user + system) / total execution time`.
`%K` | Average total memory usage of the process (data+stack+text), in `KB`.
`%w` | Number of voluntary context switches, e.g., waiting for I/O completion.
`%c` | Number of involuntary context switches (due to time slice expiration).

## References

- Linux Time Command | Linuxize <https://linuxize.com/post/linux-time-command/>
- time(1) — Arch manual pages <https://man.archlinux.org/man/time.1>
- Time - ArchWiki <https://wiki.archlinux.org/title/time>
