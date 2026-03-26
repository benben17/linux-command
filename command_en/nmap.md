nmap
===

Network exploration and security auditing tool

## Description

The **nmap command** is an open-source tool for network exploration and security auditing. It is designed to rapidly scan large networks.

### Syntax

```shell
nmap [options] [parameters]
```

### Options

```shell
-O: Enable OS detection.
-P0: Treat all hosts as online (skip host discovery).
-PT: TCP ping.
-sV: Probe open ports to determine service/version info.
-sP: Ping scan: only determine if hosts are up.
-ps: TCP SYN ping.
-PU: UDP ping.
-PE: ICMP echo discovery.
-PB: Default discovery: use ICMP echo and TCP ping.
-6: Enable IPv6 scanning.
-v: Increase verbosity.
-d: Increase debugging level.
-oN: Output scan results in normal format to the specified file.
-oX: Output scan results in XML format to the specified file.
-oM: Output in machine-readable format.
-A: Enable aggressive scan options (OS detection, version detection, script scanning, and traceroute).
--resume: Resume an aborted scan.
-p: Specify ports to scan. Can be a single port, a comma-separated list, or a range using "-".
-e: Specify the network interface to use.
-g: Use a specific port as the source port for scanning.
--ttl: Set the IPv4 time-to-live field.
--packet-trace: Show all packets sent and received.
--scanflags: Customize TCP scan flags.
--send-eth/--send-ip: Send using raw ethernet frames or raw IP packets.
```

### Parameters

Target: Specifies the IP addresses or hostnames to scan.

### Examples

**Install nmap**

```shell
yum install nmap
```

**Scan for open ports on scanme.nmap.org**

```shell
[root@localhost ~]# nmap scanme.nmap.org

Starting Nmap 7.92 ( https://nmap.org ) at 2025-08-06 15:22 CST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.37s latency).
Not shown: 991 closed tcp ports (reset)
PORT      STATE    SERVICE
22/tcp    open     ssh
80/tcp    open     http
135/tcp   filtered msrpc
139/tcp   filtered netbios-ssn
445/tcp   filtered microsoft-ds
593/tcp   filtered http-rpc-epmap
4444/tcp  filtered krb524
9929/tcp  open     nping-echo
31337/tcp open     Elite

Nmap done: 1 IP address (1 host up) scanned in 60.36 seconds
```
