vmstat
===

Display virtual memory statistics.

## Description

The **vmstat command** stands for "Virtual Memory Statistics," but it can report overall system status regarding processes, memory, I/O, and more.

### Syntax

```shell
vmstat (option) (parameter)
```

### Options

```shell
-a: Display active memory pages;
-f: Display the total number of processes created since boot;
-m: Display slab information;
-n: Display the header only once;
-s: Display event counters and memory statistics in a table format;
-d: Report disk statistics;
-p: Display statistics for a specified hard disk partition;
-S: Specify the units for output information.
```

### Parameters

*   Interval: The time interval between refreshing status information;
*   Count: The number of reports to display.

### Examples

```shell
vmstat 3
procs -----------memory---------- ---swap-- -----io---- --system-- -----cpu------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 0  0    320  42188 167332 1534368    0    0     4     7    1    0  0  0 99  0  0
 0  0    320  42188 167332 1534392    0    0     0     0 1002   39  0  0 100  0  0
 0  0    320  42188 167336 1534392    0    0     0    19 1002   44  0  0 100  0  0
 0  0    320  42188 167336 1534392    0    0     0     0 1002   41  0  0 100  0  0
 0  0    320  42188 167336 1534392    0    0     0     0 1002   41  0  0 100  0  0
```

 **Field Descriptions:** 

Procs (Processes)

*   r: The number of processes in the run queue. This value can help determine if more CPUs are needed (if consistently > 1).
*   b: The number of processes waiting for I/O.

Memory

*   swpd: Amount of virtual memory used. If swpd is non-zero but SI and SO are consistently zero, system performance is generally unaffected.
*   free: Amount of idle physical memory.
*   buff: Amount of memory used as buffers.
*   cache: Amount of memory used as cache. A high cache value indicates many files are cached; if frequently accessed files are cached, disk read I/O (bi) will be very low.

Swap

*   si: Amount of memory paged in from swap (disk to memory) per second.
*   so: Amount of memory paged out to swap (memory to disk) per second.

Note: When there is enough memory, both values are 0. If these values are consistently greater than 0, system performance may be affected as disk I/O and CPU resources are consumed. Do not worry if `free` memory is low as long as `si` and `so` remain low (mostly 0).

IO (Block size is typically 1KB in current Linux versions)

*   bi: Blocks received from a block device (read) per second.
*   bo: Blocks sent to a block device (write) per second.

Note: During random disk I/O, higher values (e.g., > 1024K) will lead to higher CPU I/O wait times.

System

*   in: Number of interrupts per second, including the clock.
*   cs: Number of context switches per second.

Note: Higher values for these two fields result in more CPU time consumed by the kernel.

CPU (Expressed as percentages)

*   us: Percentage of time spent running non-kernel code (user time). High `us` values mean user processes are consuming a lot of CPU; if consistently over 50%, consider optimizing the program.
*   sy: Percentage of time spent running kernel code (system time). High `sy` values indicate the kernel is consuming significant CPU resources, which should be investigated.
*   wa: Percentage of time spent waiting for I/O. High `wa` values indicate serious I/O waiting, possibly due to heavy random disk access or disk bottlenecks.
*   id: Percentage of time spent idle.
