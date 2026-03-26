dstat
===

Versatile tool for generating system resource statistics.

## Description

The **dstat** command is a versatile tool designed to replace `vmstat`, `iostat`, `netstat`, `nfsstat`, and `ifstat`. It is a comprehensive system information statistics tool. Compared to `sysstat`, `dstat` features a colorful interface, making performance data easier to observe manually. `dstat` also supports real-time updates; for example, `dstat 3` collects data every three seconds, with the latest data refreshed every second. Like `sysstat`, `dstat` can collect specific performance resources, such as `dstat -c` for CPU usage.

### Installation

 **Method 1** 

```shell
yum install -y dstat
```

 **Method 2** 

Download from official website: http://dag.wieers.com/rpm/packages/dstat

```shell
wget http://dag.wieers.com/rpm/packages/dstat/dstat-0.6.7-1.rh7.rf.noarch.rpm
rpm -ivh dstat-0.6.7-1.rh7.rf.noarch.rpm
```

### Usage Instructions

Once installed, `dstat` can be used for real-time monitoring of CPU, disk, network, IO, memory, etc.

Invoking `dstat` without arguments is equivalent to using the `-cdngy` parameters, which display CPU, disk, network, paging, and system information, with a 1-second interval by default. You can specify a time interval and an optional count at the end. For example, `dstat 5` displays data every 5 seconds, and `dstat 5 10` displays data every 5 seconds for a total of 10 times.

```shell
[root@iZ23uulau1tZ ~]# dstat
----total-cpu-usage---- -dsk/total- -net/total- ---paging-- ---system--
usr sys idl wai hiq siq| read  writ| recv  send|  in   out | int   csw
  0   0  99   0   0   0|7706B  164k|   0     0 |   0     0 | 189   225
  0   0 100   0   0   0|   0     0 |4436B  826B|   0     0 | 195   248
  1   0  99   0   0   0|   0     0 |4744B  346B|   0     0 | 203   242
  0   0 100   0   0   0|   0     0 |5080B  346B|   0     0 | 206   242
  0   1  99   0   0   0|   0     0 |5458B  444B|   0     0 | 214   244
  1   0  99   0   0   0|   0     0 |5080B  346B|   0     0 | 208   242
```

Explanation of some displayed information:

1.  CPU: `hiq` and `siq` are the number of hardware and software interrupts, respectively.
2.  System: `int` and `csw` are the number of system interrupts and context switches, respectively.

Other metrics are straightforward.

### Syntax

```shell
dstat [-afv] [options..] [delay [count]]
```

### Common Options

```shell
-c          Display CPU stats (system, user, idle, wait, hardware interrupt, software interrupt).
-C 0,1      Display stats for specific CPUs (e.g., cpu0 and cpu1).
-d          Display disk stats (read, write).
-D hda,total Include specific disk and total.
-n          Display network stats (receive, send).
-N eth1,total Include specific network interface and total.
-l          Display system load stats.
-m          Display memory stats (used, buffers, cache, free).
-g          Display paging stats.
-p          Display process stats (runnable, uninterruptible, new).
-s          Display swap stats.
-S          Similar to -D/-N for swap.
-r          Display I/O request stats.
-y          Display system stats (interrupts, context switches).
--ipc       Display IPC message queue and semaphore stats.
--socket    Display network socket stats (tcp, udp, raw, ip-fragments).
-a          Default option, equivalent to -cdngy.
-v          Equivalent to -pmgdsc -D total.
--output file Redirect output to a CSV file. Example: dstat --output /root/dstat.csv &
```

`dstat` has many advanced features. Refer to the `man` page for more details.

### Examples

Monitor swap, processes, sockets, and filesystem with timestamps:

```shell
[root@iZ23uulau1tZ ~]# dstat -tsp --socket --fs
----system---- ----swap--- ---procs--- ------sockets------ --filesystem-
  date/time   | used  free|run blk new|tot tcp udp raw frg|files  inodes
26-07 09:23:48|   0     0 |  0   0 0.0|104   8   5   0   0|  704   6488
26-07 09:23:49|   0     0 |  0   0   0|104   8   5   0   0|  704   6488
26-07 09:23:50|   0     0 |  0   0   0|104   8   5   0   0|  704   6489
26-07 09:23:51|   0     0 |  0   0   0|104   8   5   0   0|  704   6489
26-07 09:23:52|   0     0 |  0   0   0|104   8   5   0   0|  704   6489
26-07 09:23:53|   0     0 |  0   0   0|104   8   5   0   0|  704   6489
```

Output results to a file:

```shell
[root@iZ23uulau1tZ ~]# dstat -tsp --socket --fs --output /tmp/ds.csv
----system---- ----swap--- ---procs--- ------sockets------ --filesystem-
  date/time   | used  free|run blk new|tot tcp udp raw frg|files  inodes
26-07 09:25:31|   0     0 |  0   0 0.0|104   8   5   0   0|  736   6493
26-07 09:25:32|   0     0 |  0   0   0|104   8   5   0   0|  736   6493
26-07 09:25:33|   0     0 |  0   0   0|104   8   5   0   0|  736   6493
26-07 09:25:34|   0     0 |  0   0   0|104   8   5   0   0|  736   6493
26-07 09:25:35|   0     0 |  0   0   0|104   8   5   0   0|  736   6494
26-07 09:25:36|   0     0 |  0   0   0|104   8   5   0   0|  736   6494
```

List all available `dstat` parameters and plugins:

```shell
[root@iZ23uulau1tZ ~]# dstat --list
internal:
        aio, cpu, cpu24, disk, disk24, disk24old, epoch, fs, int, int24, io, ipc, load, lock, mem, net, page, page24, proc, raw, socket, swap, swapold, sys, tcp, time, udp, unix, vm
/usr/share/dstat:
        battery, battery-remain, cpufreq, dbus, disk-util, fan, freespace, gpfs, gpfs-ops, helloworld, innodb-buffer, innodb-io, innodb-ops, lustre, memcache-hits, mysql-io, mysql-keys, mysql5-cmds, mysql5-conn, mysql5-io, mysql5-keys,
        net-packets, nfs3, nfs3-ops, nfsd3, nfsd3-ops, ntp, postfix, power, proc-count, rpc, rpcd, sendmail, snooze, thermal, top-bio, top-cpu, top-cputime, top-cputime-avg, top-io, top-latency, top-latency-avg, top-mem, top-oom, utmp,
        vm-memctl, vmk-hba, vmk-int, vmk-nic, vz-cpu, vz-io, vz-ubc, wifi
```
