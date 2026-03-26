uptime
===

View Linux system load information.

## Description

The **uptime command** can print how long the system has been running and the system load average. The information displayed by the uptime command includes: the current time, how long the system has been running, the number of currently logged-in users, and the system load average over the past 1, 5, and 15 minutes.

### Syntax

```shell
uptime (option)
```

### Options

```shell
-V: Display version information.
```

### Examples

Use the uptime command to check the system load:

```shell
[root@LinServ-1 ~]# uptime -V    # Display uptime command version information
procps version 3.2.7

[root@LinServ-1 ~]# uptime
 15:31:30 up 127 days,  3:00,  1 user,  load average: 0.00, 0.00, 0.00
```

 **Display Content Description:** 

```shell
15:31:30             # Current system time
up 127 days, 3:00    # System uptime; a larger value indicates a more stable machine.
1 user               # Number of user connections (total connections, not distinct users)
load average: 0.00, 0.00, 0.00         # System load average for the last 1, 5, and 15 minutes
```

What is the system load average? The system load average refers to the average number of processes in the run queue over a specific time interval.

If the number of active processes per CPU core is no more than 3, system performance is good. If the number of tasks per CPU core is greater than 5, the machine's performance has serious problems.

If your Linux host has one dual-core CPU, a Load Average of 6 indicates that the machine is being fully utilized.
