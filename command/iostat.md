iostat
===

Report CPU statistics and input/output statistics for devices and partitions.

## Description

The `iostat` command is used to monitor system input/output device loading by observing the time the devices are active in relation to their average transfer rates. It reports CPU utilization and disk activity statistics. Like `vmstat`, it provides a system-wide overview rather than per-process analysis.

**iowait** indicates the percentage of time that the CPU was idle during which the system had an outstanding disk I/O request.

## Installation

`iostat` is part of the `sysstat` package.

For RedHat / CentOS / Fedora:
```bash
sudo yum install sysstat 
```

For Debian / Ubuntu / Linux Mint:
```bash
sudo apt-get install sysstat
```

## Syntax

```bash
iostat [options] [interval [count]]
```

### Options

```bash
-c         Display the CPU utilization report.
-d         Display the device utilization report (default).
-h         Make reports easier to read (human-readable).
-k         Display statistics in kilobytes per second.
-m         Display statistics in megabytes per second.
-t         Print the time for each report.
-V         Display version and exit.
-x         Display extended statistics.
-y         Omit the first report since boot if multiple intervals are displayed.
-z         Tell iostat to omit output for any devices for which there was no activity.
-j         Display persistent device names (ID, LABEL, etc.).
--human    Print sizes in human-readable format (e.g., 1.0k, 1.2M).
-o JSON    Display statistics in JSON format.
-H         Display only global statistics for groups.
-p         Display statistics for block devices and all their partitions.
```

### Parameters

- `interval`: Time in seconds between reports.
- `count`: Number of reports to generate.

## Examples

### Example 1: Basic report

```bash
# iostat
Linux 4.18.0 (node1) 	08/28/2024 	_x86_64_	(2 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           3.30    0.01    1.90    0.12    0.00   94.68

Device             tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
vda               7.85        84.22        36.59 1081853831  470049100
```

**CPU Report Metrics:**
- `%user`: CPU utilization at the user level.
- `%nice`: CPU utilization at the user level with nice priority.
- `%system`: CPU utilization at the system (kernel) level.
- `%iowait`: Time the CPU was idle with outstanding I/O requests.
- `%steal`: Time spent in involuntary wait by the virtual CPU.
- `%idle`: Time the CPU was idle with no outstanding I/O requests.

**Device Report Metrics:**
- `Device`: Name of the device or partition.
- `tps`: Transfers per second.
- `kB_read/s`: Data read from the device in kB/s.
- `kB_wrtn/s`: Data written to the device in kB/s.
- `kB_read`: Total kB read.
- `kB_wrtn`: Total kB written.

### Example 2: Human-readable extended report, ignoring first report, every 1s for 5 times

```bash
# iostat -hdy 1 5
```

### Example 3: Extended statistics

```bash
# iostat -xd 1
```

**Extended Metrics:**
- `r/s`: Read requests per second.
- `w/s`: Write requests per second.
- `rrqm/s`: Read requests merged per second.
- `wrqm/s`: Write requests merged per second.
- `r_await`: Average time (ms) for read requests to be served.
- `w_await`: Average time (ms) for write requests to be served.
- `aqu-sz`: Average queue length of requests.
- `%util`: Percentage of CPU time during which I/O requests were issued (bandwidth utilization).

When `%iowait` is high, pay attention to `%util` (close to 100% indicates a bottleneck) and `await` values.
