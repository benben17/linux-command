top
===

Display or manage running processes

## Description

The **top command** allows real-time dynamic viewing of the overall system operation. it is a comprehensive tool for monitoring system performance and operational information from multiple aspects. Through the interactive interface provided by the top command, you can manage processes using hotkeys.

### Syntax

```shell
top [options]
```

### Options

```shell
-b: Operate in batch mode;
-c: Display complete command lines;
-d: Screen refresh interval;
-I: Ignore idle processes;
-s: Secure mode;
-S: Cumulative mode;
-i <time>: Set interval time;
-u <username>: Specify username;
-p <pid>: Specify process ID;
-n <count>: Number of iterations to display;
-H: Resource usage for all threads.
```

### top Interactive Commands

Interactive commands available during top execution. These are single-letter commands. Some may be disabled if the `-s` option was used on the command line.

```shell
h: Display help screen with a brief command summary;
k: Terminate a process;
i: Ignore idle and zombie processes (toggle);
q: Quit the program;
r: Reschedule a process priority;
S: Switch to cumulative mode;
s: Change delay between refreshes (in seconds; decimals are converted to ms). Entering 0 causes continuous refresh. Default is 5s;
f or F: Add or remove items from the current display;
o or O: Change the order of displayed items;
l: Toggle display of load average and uptime information;
m: Toggle display of memory information;
t: Toggle display of process and CPU status information;
c: Toggle display of command name and full command line;
M: Sort by resident memory size;
P: Sort by CPU usage percentage;
T: Sort by time/cumulative time;
w: Write current settings to the ~/.toprc file.
```

### Example

```shell
top - 09:44:56 up 16 days, 21:23,  1 user,  load average: 9.59, 4.75, 1.92
Tasks: 145 total,   2 running, 143 sleeping,   0 stopped,   0 zombie
Cpu(s): 99.8%us,  0.1%sy,  0.0%ni,  0.2%id,  0.0%wa,  0.0%hi,  0.0%si,  0.0%st
Mem:   4147888k total,  2493092k used,  1654796k free,   158188k buffers
Swap:  5144568k total,       56k used,  5144512k free,  2013180k cached
```

**Explanation:**

* top - 09:44:56 [current system time],
* 16 days [system uptime],
* 1 user [number of logged-in users],
* load average: 9.59, 4.75, 1.92 [system load; average length of the task queue]
* Tasks: 145 total [total number of processes],
* 2 running [number of running processes],
* 143 sleeping [number of sleeping processes],
* 0 stopped [number of stopped processes],
* 0 zombie [number of zombie processes],
* Cpu(s): 99.8%us [CPU percentage used by user space],
* 0.1%sy [CPU percentage used by kernel space],
* 0.0%ni [CPU percentage used by processes with changed priority in user space],
* 0.2%id [CPU percentage idle],
* 0.0%wa [CPU percentage waiting for I/O],
* 0.0%hi [hardware interrupts],
* 0.0%st [steal time],
* Mem: 4147888k total [total physical memory],
* 2493092k used [total physical memory used],
* 1654796k free [total physical memory free],
* 158188k buffers [memory used for kernel buffers]
* Swap: 5144568k total [total swap space],
* 56k used [total swap space used],
* 5144512k free [total swap space free],
* 2013180k cached [total swap space cached]
