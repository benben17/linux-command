pidstat
===

Monitors system resource usage for individual processes.

## Description

**pidstat** is a command from the `sysstat` toolset. it is used to monitor the utilization of system resources (CPU, memory, threads, device I/O, etc.) for all or specific processes.

When run for the first time, `pidstat` displays statistics since system startup. Subsequent runs show statistics since the previous run. Users can specify the number of reports and the time interval between them.

### Syntax

```shell
pidstat [options] [interval [count]]
```

### Options

- `-u`: (Default) Display CPU utilization for each process.
- `-r`: Display memory utilization.
- `-d`: Display I/O statistics.
- `-w`: Display context switching activity.
- `-t`: Display statistics for threads associated with the selected tasks.
- `-p <pid>`: Monitor only the specified process ID.
- `-T { TASK | CHILD | ALL }`:
  - `TASK`: Report independent tasks (default).
  - `CHILD`: Report cumulative statistics for a process and all its children.
  - `ALL`: Report both.
- `-V`: Print version number.
- `-h`: Display all activities on a single line for easier parsing by other programs.
- `-I`: In an SMP environment, report CPU usage divided by the total number of processors.
- `-l`: Display the command name and all its arguments.

### Examples

#### View CPU usage for all processes

```shell
# pidstat -u -p ALL
11:04:06 AM   UID       PID    %usr %system  %guest    %CPU   CPU  Command
11:04:06 AM     0         1    0.03    0.05    0.00    0.08    20  systemd
...
```

**Header Meanings:**
- `PID`: Process ID.
- `%usr`: Percentage of CPU used by the process at the user level.
- `%system`: Percentage of CPU used by the process at the kernel level.
- `%guest`: Percentage of CPU used by the process in a virtual machine.
- `%CPU`: Total percentage of CPU time used by the process.
- `CPU`: Processor number the process is running on.
- `Command`: The command associated with the process.

#### View memory usage for all processes

```shell
# pidstat -r
11:10:35 AM   UID       PID  minflt/s  majflt/s     VSZ    RSS   %MEM  Command
11:10:35 AM     0         1      7.24      0.05  191312   4208   0.01  systemd
...
```

**Header Meanings:**
- `minflt/s`: Minor page faults per second (those that don't require loading from disk).
- `majflt/s`: Major page faults per second (those that require loading from disk).
- `VSZ`: Virtual size (KB) of the entire task.
- `RSS`: Resident Set Size (KB) - non-swapped physical memory used.

#### View I/O usage for all processes

```shell
# pidstat -d
11:12:30 AM   UID       PID   kB_rd/s   kB_wr/s kB_ccwr/s  Command
11:12:30 AM     0         1    250.05     11.57      2.13  systemd
...
```

**Header Meanings:**
- `kB_rd/s`: Kilobytes read from disk per second.
- `kB_wr/s`: Kilobytes written to disk per second.
- `kB_ccwr/s`: Kilobytes whose writing to disk has been cancelled (e.g., when a task truncates a dirty pagecache).

#### View context switching activity

```shell
# pidstat -w
11:15:52 AM   UID       PID   cswch/s nvcswch/s  Command
11:15:52 AM     0         1      3.15      0.03  systemd
...
```

**Header Meanings:**
- `cswch/s`: Number of voluntary context switches per second.
- `nvcswch/s`: Number of non-voluntary context switches per second.
