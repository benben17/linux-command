atop
===

Tool for monitoring Linux system resources and processes

## Additional Information

The **atop command** is an open-source system monitoring tool that records the operating status of the system at a certain frequency. The collected data includes system resource usage (CPU, memory, disk, and network) and process operation status, and can be saved to the disk in the form of log files. When a problem occurs on the server, we can obtain the corresponding atop log files for analysis. atop is open-source software, and you can get its [source code](https://github.com/Atoptool/atop) and [RPM installation packages](https://pkgs.org/download/atop) from their respective links.

## Syntax

```shell
atop [options] [parameters]
```

## Description

### ATOP Column

This column shows the hostname, sampling date, and time.

### PRC Column

This column shows the overall running status of processes:

- `sys` and `usr` fields indicate the running time of processes in kernel mode and user mode, respectively.
- `#proc` field indicates the total number of processes.
- `#zombie` field indicates the number of zombie processes.
- `#exit` field indicates the number of processes that exited during the atop sampling period.

### CPU Column

This column shows the overall usage of the CPU (i.e., multi-core CPU as a whole CPU resource):

- `sys` and `usr` fields indicate the proportion of CPU time used for processing processes in kernel mode and user mode.
- `irq` field indicates the proportion of CPU time used for handling interrupts.
- `idle` field indicates the proportion of time the CPU is completely idle.
- `wait` field indicates the proportion of time the CPU is idle because processes are waiting for disk I/O.

The sum of the values in the CPU column is N00%, where N is the number of CPU cores.

### cpu Column

This column shows the usage of a specific CPU core. The meaning of each field is the same as in the CPU column, and the sum of the fields is 100%.

### CPL Column

This column shows the CPU load status:

- `avg1`, `avg5`, and `avg15` fields: The average number of processes in the run queue over the past 1, 5, and 15 minutes.
- `csw` field indicates the number of context switches.
- `intr` field indicates the number of interrupts.

### MEM Column

This column indicates memory usage:

- `tot` field indicates the total amount of physical memory.
- `free` field indicates the amount of free memory.
- `cache` field indicates the amount of memory used for page cache.
- `buff` field indicates the amount of memory used for file cache.
- `slab` field indicates the amount of memory occupied by the system kernel.

### SWP Column

This column indicates swap space usage:

- `tot` field indicates the total amount of swap space.
- `free` field indicates the amount of free swap space.

### PAG Column

This column indicates virtual memory paging status:

- `swin` and `swout` fields: The number of memory pages swapped in and out.

### DSK Column

This column indicates disk usage. Each disk device corresponds to a column. If there is an `sdb` device, an additional DSK column is added:

- `sda` field: Disk device identifier.
- `busy` field: Proportion of time the disk is busy.
- `read` and `write` fields: The number of read and write requests.

### NET Column

Multiple NET columns show network status, including the transport layer (TCP and UDP), IP layer, and information for each active network interface:

- `XXXi` field indicates the number of received packets for each layer or active network interface.
- `XXXo` field indicates the number of sent packets for each layer or active network interface.

## atop Logs

A series of sampled pages over time forms an atop log file. We can use the `atop -r XXX` command to view the log file. Log files are saved as follows:

- One atop log file is saved every day, recording information for that day.
- Log files are named in the format `atop_YYYYMMDD`.
- A log expiration period is set to automatically delete log files from a certain time ago.

The atop developers provide the above log saving methods, and the corresponding `atop.daily` script can be found in the source directory. In the `atop.daily` script, we can change the atop sampling period (default is 10 minutes) by modifying the `INTERVAL` variable; we can change the log retention period (default is 28 days) by modifying the numerical value in the following command:

```shell
(sleep 3; find $LOGPATH -name 'atop_*' -mtime +28 -exec rm {} \; )& 
```

Finally, we can modify the cron file to execute the `atop.daily` script every day at midnight:

```shell
0 0 * * * root /etc/cron.daily/atop.daily
```

## Related Resources

- [Official Manual](http://www.atoptool.nl/download/man_atop-1.pdf)
