clockdiff
===

Measure the time difference between two Linux hosts

## Description

Timestamp data can be placed in the headers of IP and ICMP packets. The **clockdiff** program uses these timestamps to measure the system time difference between the destination host and the local host.

### Options

```shell
-o: Use the IP timestamp option to measure the system time difference. Uses 3 timestamps.
-o1: Use the IP timestamp option to measure the system time difference. Uses 4 timestamps. If neither -o nor -o1 is set, ICMP timestamps are used.
```

### Examples

```shell
lixi@lixi-desktop:~$ ping -T tsandaddr www.ustc.edu.cn -c 1
PING www.ustc.edu.cn (202.38.64.9) 56(124) bytes of data.
64 bytes from 202.38.64.9: icmp_seq=1 ttl=62 time=0.823 ms
TS:     lixi-desktop.local (210.45.74.25)    12522473 absolute
    210.45.74.1    -251
    local-gw.ustc.edu.cn (202.38.64.126)    248
    202.38.64.9    -857514
Unrecorded hops: 3

--- www.ustc.edu.cn ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.823/0.823/0.823/0.000 ms
```

From the above, when the RTT is small, the relationship between ICMP timestamps can be determined. The time difference between the local host and 202.38.64.9 is approximately: -857514 + 248 - 251 = -857517. Test the system time of the route using both the `-o` option (IP timestamp) and without any option (ICMP timestamp). Results:

```shell
lixi@lixi-desktop:~# ./clockdiff -o 202.38.64.9  
..................................................
host=202.38.64.9 rtt=1(0)ms/1ms delta=-857517ms/-857517ms Wed Dec 17 11:28:30 2008
```

```shell
lixi@lixi-desktop:~# ./clockdiff 202.38.64.9
.
host=202.38.64.9 rtt=750(187)ms/0ms delta=-857517ms/-857517ms Wed Dec 17 11:28:35 2008
```

Both methods are relatively accurate.

```shell
lixi@lixi-desktop:~# ./clockdiff gigagate1.Princeton.EDU
..................................................
host=gigagate1.Princeton.EDU rtt=307(21)ms/271ms delta=-5ms/-5ms Wed Dec 17 11:50:16 2008
```

The above example measures the time difference with a destination host that has a larger RTT. Note that using `clockdiff` requires some luck, as many routers ignore ICMP or IP timestamps.
