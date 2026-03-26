tcpdump
===

A powerful command-line packet sniffer and network analyzer

## Description

The **tcpdump command** is a packet sniffer tool that prints the headers of packets on a network interface. It can also save packet data to a file for later analysis using the `-w` option.

### Syntax 

```shell
tcpdump (options)
```

### Options 

```shell
-a: Attempt to convert network and broadcast addresses to names.
-c <count>: Stop after receiving <count> packets.
-d: Dump the compiled packet-matching code in a human-readable format to stdout.
-dd: Dump packet-matching code as a C program fragment.
-ddd: Dump packet-matching code as decimal numbers.
-e: Print the link-level header on each dump line.
-f: Print internet addresses numerically.
-F <file>: Use <file> as input for the filter expression.
-i <interface>: Listen on <interface>.
-l: Make stdout line buffered.
-n: Do not convert host addresses to names.
-N: Do not print domain name qualification of host names.
-O: Do not run the packet-matching code optimizer.
-p: Do not put the interface into promiscuous mode.
-q: Quick output. Print less protocol information.
-r <file>: Read packets from <file>.
-s <snaplen>: Set the packet snapshot length.
-S: Print absolute, rather than relative, TCP sequence numbers.
-t: Do not print a timestamp on each dump line.
-tt: Print an unformatted timestamp on each dump line.
-T <type>: Force packets selected by "expression" to be interpreted as the specified type.
-v: Verbose output.
-vv: Even more verbose output.
-x: Print each packet (minus its link level header) in hex.
-w <file>: Write the raw packets to <file> rather than parsing and printing them.
```

### Examples 

**Monitor all packets on the first network interface**

```shell
tcpdump
```

**Monitor a specific network interface**

```shell
tcpdump -i eth1
```

If no interface is specified, `tcpdump` defaults to the first interface (usually `eth0`).

**Monitor packets for a specific host**

Print all packets arriving at or leaving `sundown`:

```shell
tcpdump host sundown
```

Specify an IP address:

```shell
tcpdump host 210.27.48.1
```

Print packets between `helios` and either `hot` or `ace`:

```shell
tcpdump host helios and \( hot or ace \)
```

Intercept communication between `210.27.48.1` and either `210.27.48.2` or `210.27.48.3`:

```shell
tcpdump host 210.27.48.1 and \( 210.27.48.2 or 210.27.48.3 \)
```

Print IP packets between `ace` and any other host, excluding `helios`:

```shell
tcpdump ip host ace and not helios
```

**Monitor specific host and port**

To capture Telnet packets for host `210.27.48.1`:

```shell
tcpdump tcp port 23 and host 210.27.48.1
```

Monitor UDP port 123 (NTP):

```shell
tcpdump udp port 123
```

**Monitor a specific network**

Print all traffic between the local host and the Berkeley network:

```shell
tcpdump net ucb-ether
```

Print all FTP traffic through gateway `snup`:

```shell
tcpdump 'gateway snup and (port ftp or ftp-data)'
```
Note: The expression is enclosed in single quotes to prevent the shell from misinterpreting the parentheses.

**Capture HTTP packets on port 80 and display as text**

```shell
sudo tcpdump -i any port 80 -A
```
