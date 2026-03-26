hwclock
===

Display and set the hardware clock (RTC).

## Description

The `hwclock` command is a utility for accessing the hardware clock. It can display the current time, set the hardware clock, and synchronize time between the hardware clock and the system (kernel) clock.

In Linux, there are two clocks: the hardware clock and the system clock. The hardware clock refers to the physical clock on the motherboard, often configurable in the BIOS. The system clock is maintained by the Linux kernel. During startup, the kernel reads the hardware clock to initialize the system clock. After that, they operate independently. Linux commands and functions primarily interact with the system clock.

### Syntax

```shell
hwclock [options]
```

### Options

```shell
--adjust : Adjust the hardware clock for systematic drift based on records in /etc/adjtime.
--debug : Display detailed information about hwclock's execution.
--directisa : Access the hardware clock directly via I/O instructions instead of /dev/rtc.
--hctosys : Set the system clock from the hardware clock.
--set --date=<date_and_time> : Set the hardware clock to a specific time.
--show : Display the current hardware clock date and time.
--systohc : Set the hardware clock from the system clock.
--test : Test mode; does not actually change any clock settings.
--utc : Use Coordinated Universal Time (UTC) for the hardware clock.
--version : Display version information.
```

### Examples

Synchronize the hardware clock from the system clock:

```shell
hwclock --systohc
hwclock --systohc --utc
```

Display the current hardware date and time:

```shell
hwclock
```

Check the clock configuration file (Debian/Ubuntu example):

```shell
cat /etc/default/rcS 
UTC=yes
```

Check the configuration on other distributions (RedHat/CentOS example):

```shell
cat /etc/sysconfig/clock
ZONE="America/Los_Angeles"
UTC=false
ARC=false
```
