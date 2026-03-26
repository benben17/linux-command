sar
===

System activity reporting tool.

## Description

The **sar command** is a system activity reporting tool under Linux that displays specified operating system state counters to the standard output device. The `sar` tool samples the current state of the system and then expresses the system's current operating state by calculating data and ratios. Its characteristic is that it can continuously sample the system to obtain a large amount of sampling data. Both sampling data and analysis results can be stored in files, and it consumes very few system resources when used.

### Syntax

```shell
sar(options)(parameters)
```

### Options

```shell
-A: Displays all report information.
-b: Displays I/O rates.
-B: Displays paging statistics.
-c: Displays process creation activity.
-d: Displays the status of each block device.
-e: Sets the end time for the report.
-f: Extracts the report from the specified file.
-i: Sets the interval for refreshing status information.
-n: Reports network statistics.
-P: Reports status for each CPU.
-R: Displays memory statistics.
-u: Displays CPU utilization.
-v: Displays the status of inodes, files, and other kernel tables.
-w: Displays swapping statistics.
-x: Displays the status of a given process.
```

```shell
-r: Displays output in pages, with a maximum of 100 lines per page.
-o: Output options; specifies the columns to be displayed. E.g., `-o mrk,prt,cvg` displays CPU usage, PIDs, disk usage, and network traffic.
-t: Timestamp option; adds timestamps to the output.
-s: Statistics option; specifies the type of statistics to display. E.g., `-s us,ms` displays average values for us and ms CPU time.
-c: Specifies the command to be sent. E.g., `-c ls` displays the list of files and subdirectories in the current directory.
```

### Parameters

*   Interval: The interval between reports in seconds.
*   Count: The number of reports to display.

### Examples

**Check memory and swap space utilization:**

```shell
sar -r
Linux 2.4.20-8 (www.jsdig.com)    20130503  
12:00:01 AM kbmemfree kbmemused  %memused 
kbmemshrd kbbuffers  kbcached  
12:10:00 AM    240468   1048252     81.34    
0    133724    485772  
12:20:00 AM    240508   1048212     81.34   
0    134172    485600  
…  
08:40:00 PM    934132    354588     27.51    
0     26080    185364  
Average:       324346    964374     74.83  
0     96072    467559 
```

The `kbmemfree` and `kbmemused` fields show unused and used memory, respectively, followed by the percentage of used memory (`%memused`). The `kbbuffers` and `kbcached` fields show the amount of data accessed by buffers and the system cache, respectively, in KB.

**Monitor system components for 10 minutes and sort the data:**

```shell
sar -o temp 60 10
```

**Display memory and network statistics stored in the daily data file "sa16":**

```shell
sar -r -n DEV -f /var/log/sa/sa16
```

**Check CPU utilization:**

```shell
sar -t
```

**Check disk utilization:**

```shell
sar -s disk
```

**Check network traffic:**

```shell
sar -s nic
```

**Send a command to a system service:**

```shell
sar -c ls
```

**Display the current system timestamp:**

```shell
sar -t +%s
```

These are just a few examples of the `sar` command; you can choose different options and parameters based on your specific needs.

Note: The output of the `sar` command may vary depending on system performance. For more accurate results, consider monitoring when system performance is optimal.
