fping
===

A tool to check if hosts are alive.

## Description

The **fping command** is similar to `ping` but much more powerful. Unlike `ping`, which waits for a response or a timeout from a single host before moving to the next, `fping` sends a packet to one host and immediately moves to the next. This allows it to ping multiple hosts simultaneously. `fping` also allows specifying a range of IP addresses or a list of hosts via the command line.

### Syntax

```shell
fping (options) (parameters)
```

### Options

```shell
-a  # Show systems that are alive.
-b  # Size of the ping packet (default is 56 bytes).
-c  # Number of pings to send to each target (default is 1).
-f  # Read a list of targets from a file (cannot be used with -g).
-l  # Loop mode (send pings continuously).
-g  # Generate a target list by specifying start and end addresses (can be a network range).
-u  # Show targets that are unreachable.
```

### Examples

Installing `fping`:

```shell
# Install EPEL repository first:
yum install epel* -y
# Install fping package:
yum install fping -y
```

Ping specific IP addresses:

```shell
~]# fping 192.168.0.1 192.168.0.125 192.168.0.126 2>/dev/null
192.168.0.1 is alive
192.168.0.125 is alive
192.168.0.126 is unreachable
```

Ping an entire network segment:

```bash
~]# fping -g 192.168.0.0/24 2>/dev/null
192.168.0.1 is alive
192.168.0.103 is alive
...
192.168.0.253 is unreachable
192.168.0.254 is unreachable
```

Ping a network segment and show only alive hosts:

```shell
~]# fping -ag 192.168.0.0/24 2>/dev/null
192.168.0.1
192.168.0.103
...
```

Ping a specific range of IPs:

```shell
~]# fping -ag 192.168.0.5 192.168.0.130 2>/dev/null
192.168.0.103
...
192.168.0.125
192.168.0.130
```
