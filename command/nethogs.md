nethogs
===

Terminal-based network traffic monitoring tool

## Description

There are many open-source network monitoring tools for Linux. For example, you can use `iftop` to check bandwidth usage, `netstat` to view interface statistics, and `top` to monitor running processes. However, if you are looking for a tool that provides real-time network bandwidth usage per process, **NetHogs** is worth a look.

**NetHogs** is an open-source command-line tool (similar to the Linux `top` command) used to track real-time network bandwidth usage per process or program.

From the NetHogs project website:

> NetHogs is a small 'net top' tool. Instead of breaking the traffic down per protocol or per subnet, like most tools do, it groups bandwidth by process. NetHogs does not rely on a special kernel module to be loaded. If there's suddenly a lot of network traffic, you can fire up NetHogs and immediately see which PID is causing this. This makes it easy to identify programs that have gone wild and are suddenly taking up your bandwidth.

This article introduces how to install and use NetHogs to monitor network bandwidth usage per process on Unix/Linux operating systems.

### Syntax

```shell
nethogs [options] [device [device [device ...]]]
```

### Options

```shell
usage: nethogs [-V] [-h] [-b] [-d seconds] [-v mode] [-c count] [-t] [-p] [-s] [device [device [device ...]]]
  -V : Print version.
  -h : Print this help message.
  -b : Bughunt mode - implies tracemode.
  -d : Delay for update refresh rate (in seconds). Default is 1.
  -v : View mode (0 = KB/s, 1 = total KB, 2 = total B, 3 = total MB). Default is 0.
  -c : Number of updates. Default is 0 (unlimited).
  -t : Trace mode.
  -p : Promiscuous mode (not recommended).
  -s : Sort output by the SENT column.
  -a : Monitor all devices, even loopback/stopped.
  device : Device(s) to monitor. Default is all active interfaces except loopback.

While nethogs is running, press:
  q: Quit
  s: Sort by SENT traffic
  r: Sort by RECEIVE traffic
  m: Toggle between total (KB, B, MB) and KB/s modes
```

**Common Parameters**

*   `-d`: Refresh interval.
*   `-h`: Help.
*   `-p`: Promiscuous mode.
*   `-t`: Trace mode.
*   `-V`: Version.

**Interactive Commands**

*   `m`: Cycle through units (KB/s, KB, B, MB).
*   `r`: Sort by received traffic.
*   `s`: Sort by sent traffic.
*   `q`: Exit the program.

### Installation

**On RHEL, CentOS, and Fedora**

To install NetHogs, you must enable the EPEL repository for your version of Linux. Then run the following `yum` command:

```shell
yum install nethogs
```

**On Ubuntu, Linux Mint, and Debian**

Use the `apt-get` command:

```shell
sudo apt-get install nethogs
```

### Usage

On RedHat-based systems, start the tool with:

```shell
nethogs
```

On Debian/Ubuntu/Linux Mint, you must have root privileges:

```shell
sudo nethogs
```

**Preview of NetHogs on Ubuntu 12.10**

As shown in the interface, the `SENT` and `RECEIVED` columns display traffic statistics for each process. Total bandwidth is shown at the bottom. You can use interactive commands to control the sorting.

### Command Line Arguments

You can use `-d` to set the refresh rate and specify device names to monitor specific interfaces (default is eth0). For example, to set a 5-second refresh rate:

```shell
sudo nethogs -d 5
```

To monitor only the `eth0` interface:

```shell
sudo nethogs eth0
```

To monitor both `eth0` and `eth1` interfaces:

```shell
sudo nethogs eth0 eth1
```

For a complete list of parameters, refer to the NetHogs manual by typing `man nethogs` in your terminal. For more information, visit the NetHogs project homepage.
