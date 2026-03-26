mpstat
===

Display statistics for each available CPU

## Description

The **mpstat command** is primarily used in multi-processor environments to display statistics for each available CPU. This information is sourced from the `/proc/stat` file. In multi-CPU systems, it can display both average statistics across all CPUs and details for specific individual CPUs.

### Syntax

```shell
mpstat [options] [<interval> [<count>]]
```

### Options

```shell
-P: Specify the CPU number (or "ALL").
```

### Parameters

- interval: Time in seconds between each report.
- count: Number of reports to generate.

### Column Meanings
- %user: Percentage of CPU utilization that occurred while executing at the user level (application).
- %nice: Percentage of CPU utilization that occurred while executing at the user level with nice priority.
- %system: Percentage of CPU utilization that occurred while executing at the system level (kernel).
- %iowait: Percentage of time that the CPU or CPUs were idle during which the system had an outstanding disk I/O request.
- %irq: Percentage of time spent by the CPU or CPUs to service hardware interrupts.
- %soft: Percentage of time spent by the CPU or CPUs to service software interrupts.
- %steal: Percentage of time spent in involuntary wait by the virtual CPU or CPUs while the hypervisor was servicing another virtual processor.
- %guest: Percentage of time spent by the CPU or CPUs to run a virtual processor.
- %gnice: Percentage of time spent by the CPU or CPUs to run a niced guest.
- %idle: Percentage of time that the CPU or CPUs were idle and the system did not have an outstanding disk I/O request.

### Examples

When `mpstat` is run without parameters, it displays average values since system startup.

```shell
mpstat
Linux 3.10.0-1160.71.1.el7.x86_64 (centos)      08/14/2022      _x86_64_        (4 CPU)

04:28:36 PM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
04:28:36 PM  all    0.03    0.00    0.07    0.00    0.00    0.01    0.00    0.00    0.00   99.89
```

**Generate reports for all processors every 2 seconds:**

The following command generates statistics for all processors every 2 seconds, for a total of three intervals, followed by an average of those three intervals. By default, output is sorted by CPU number. The first line of each interval shows the combined utilization of all processors (`all`).

```shell
mpstat -P ALL 2 3
Linux 3.10.0-1160.71.1.el7.x86_64 (centos)      08/15/2022      _x86_64_        (4 CPU)

09:32:43 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
09:32:45 AM  all    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
09:32:45 AM    0    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
09:32:45 AM    1    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
09:32:45 AM    2    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
09:32:45 AM    3    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00

09:32:45 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
09:32:47 AM  all    0.00    0.00    0.12    0.00    0.00    0.12    0.00    0.00    0.00   99.75
09:32:47 AM    0    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
09:32:47 AM    1    0.00    0.00    0.50    0.00    0.00    0.00    0.00    0.00    0.00   99.50
09:32:47 AM    2    0.00    0.00    0.00    0.00    0.00    0.50    0.00    0.00    0.00   99.50
09:32:47 AM    3    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00

09:32:47 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
09:32:49 AM  all    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
09:32:49 AM    0    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
09:32:49 AM    1    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
09:32:49 AM    2    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
09:32:49 AM    3    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00

Average:     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
Average:     all    0.00    0.00    0.04    0.00    0.00    0.04    0.00    0.00    0.00   99.92
Average:       0    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
Average:       1    0.00    0.00    0.17    0.00    0.00    0.00    0.00    0.00    0.00   99.83
Average:       2    0.00    0.00    0.00    0.00    0.00    0.17    0.00    0.00    0.00   99.83
Average:       3    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
```

**Comparing results with and without parameters:**

Performing a stress test on localhost:

```shell
ping -f localhost
```

Then run `mpstat` in another terminal:

```shell
mpstat
Linux 3.10.0-1160.71.1.el7.x86_64 (centos)      08/15/2022      _x86_64_        (4 CPU)

09:34:20 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
09:34:20 AM  all    0.03    0.00    0.07    0.00    0.00    0.02    0.00    0.00    0.00   99.88
```

As mentioned before, without parameters, `mpstat` displays the average since startup, so you might not see immediate changes.

To see real-time CPU usage during a specific period, you must specify an interval:

```shell
mpstat 3 10
Linux 3.10.0-1160.71.1.el7.x86_64 (centos)      08/15/2022      _x86_64_        (4 CPU)

09:36:21 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
09:36:24 AM  all    1.81    0.00    7.03    0.00    0.00    6.37    0.00    0.00    0.00   84.79
09:36:27 AM  all    1.82    0.00    6.88    0.00    0.00    5.83    0.00    0.00    0.00   85.47
09:36:30 AM  all    1.95    0.00    5.86    0.00    0.00    4.98    0.00    0.00    0.00   87.21
09:36:33 AM  all    3.95    0.00    6.50    0.00    0.00    5.46    0.00    0.00    0.00   84.09
09:36:36 AM  all    4.05    0.00    6.21    0.00    0.00    5.64    0.00    0.00    0.00   84.10
09:36:39 AM  all    4.21    0.00    6.92    0.00    0.00    5.33    0.00    0.00    0.00   83.54
09:36:42 AM  all    3.72    0.00    7.17    0.00    0.00    6.05    0.00    0.00    0.00   83.05
09:36:45 AM  all    3.97    0.00    6.93    0.00    0.00    6.65    0.00    0.00    0.00   82.46
09:36:48 AM  all    4.30    0.00    9.55    0.00    0.00    9.55    0.00    0.00    0.00   76.59
09:36:51 AM  all    4.35    0.00    9.31    0.00    0.00    8.79    0.00    0.00    0.00   77.55
Average:     all    3.44    0.00    7.28    0.00    0.00    6.52    0.00    0.00    0.00   82.76
```

This demonstrates that to correctly reflect system status, you must use command parameters appropriately. The same applies to `vmstat` and `iostat`.
