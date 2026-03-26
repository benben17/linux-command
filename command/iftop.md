iftop
===

A real-time network bandwidth monitoring tool.

## Description

The `iftop` command is a real-time traffic monitoring tool that displays bandwidth usage on network interfaces, including TCP/IP connections. It lacks reporting features and must be run as root.

### Syntax

```shell
iftop [options]
```

### Options

```shell
-h                  Display help message.
-n                  Do not resolve IP addresses to hostnames.
-N                  Do not resolve port numbers to service names.
-p                  Run in promiscuous mode (show traffic between other hosts on the same segment).
-b                  Do not display the traffic bar graph.
-B                  Display bandwidth in bytes instead of bits.
-i interface        Monitor a specific network interface (e.g., -i eth0).
-f filter code      Use filter code to select packets to count.
-F net/mask         Show traffic for a specific IPv4 network.
-G net6/mask6       Show traffic for a specific IPv6 network.
-l                  Show local/loopback/IPv6 traffic (default: off).
-P                  Show host ports.
-m limit            Set the upper limit for the bandwidth scale.
-c config file      Specify an optional configuration file.
-t                  Use text-only mode.

Sorting:
-o 2s               Sort by the first column (2s average).
-o 10s              Sort by the second column (10s average).
-o 40s              Sort by the third column (40s average).
-o source           Sort by source address.
-o destination      Sort by destination address.

Text mode only:
-s num              Print one output after num seconds, then exit.
-L num              Number of lines to print.
```

### Interface Description

- The first line shows the bandwidth scale (e.g., 1Mbit).
- The main list shows connections. The last three columns are traffic averages over 2, 10, and 40 seconds.
- `=>` indicates sent traffic.
- `<=` indicates received traffic.
- The last three rows show the sum of sent, received, and total traffic.
- The columns show cumulative total, peak values, and average values.

### Examples

```shell
iftop           # Monitor the first network interface.
iftop -i eth1   # Monitor eth1.
iftop -n        # Show IPs directly without DNS lookup.
iftop -N        # Show port numbers without service names.
iftop -F 192.168.1.0/24  # Show traffic for a specific subnet.
```
