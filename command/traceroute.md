traceroute
===

Display the path that data packets take to reach a host

## Description

The **traceroute command** is used to trace the full path that data packets take while transmitting over the network. By default, it sends packets with a size of 40 bytes.

Through traceroute, we can understand the path information takes from your computer to a host on the other side of the Internet. While the path taken by packets from a specific source to a specific destination may vary, the route is usually the same.

traceroute measures how long it takes for small data packets to be sent to a destination device and returned. For each device on a path, traceroute performs three measurements. The output includes the time for each test (in ms), the name of the device (if available), and its IP address.

### Syntax

```shell
traceroute [options] [parameters]
```

### Options

```shell
-d: Enable socket-level debugging;
-f<ttl>: Set the initial time-to-live (TTL) value for the first probe packet;
-F: Set the "Don't Fragment" bit;
-g<gateway>: Set source route gateways (up to 8);
-i<interface>: Use the specified network interface to send packets;
-I: Use ICMP ECHO instead of UDP datagrams;
-m<max_ttl>: Set the maximum time-to-live (TTL) for probe packets;
-n: Use IP addresses directly instead of hostnames;
-p<port>: Set the UDP port for transmission;
-r: Bypass normal routing tables and send directly to the remote host;
-s<source_addr>: Set the source IP address for outgoing packets;
-t<tos>: Set the Type of Service (TOS) value for probe packets;
-v: Verbose output;
-w<timeout>: Set the time (in seconds) to wait for a response;
-x: Enable or disable packet checksum validation.
```

### Parameters

Host: Specifies the destination IP address or hostname.

### Examples

```shell
traceroute www.58.com
traceroute to www.58.com (211.151.111.30), 30 hops max, 40 byte packets
 1  unknown (192.168.2.1)  3.453 ms  3.801 ms  3.937 ms
 2  221.6.45.33 (221.6.45.33)  7.768 ms  7.816 ms  7.840 ms
 3  221.6.0.233 (221.6.0.233)  13.784 ms  13.827 ms 221.6.9.81 (221.6.9.81)  9.758 ms
 4  221.6.2.169 (221.6.2.169)  11.777 ms 122.96.66.13 (122.96.66.13)  34.952 ms 221.6.2.53 (221.6.2.53)  41.372 ms
 5  219.158.96.149 (219.158.96.149)  39.167 ms  39.210 ms  39.238 ms
 6  123.126.0.194 (123.126.0.194)  37.270 ms 123.126.0.66 (123.126.0.66)  37.163 ms  37.441 ms
 7  124.65.57.26 (124.65.57.26)  42.787 ms  42.799 ms  42.809 ms
 8  61.148.146.210 (61.148.146.210)  30.176 ms 61.148.154.98 (61.148.154.98)  32.613 ms  32.675 ms
 9  202.106.42.102 (202.106.42.102)  44.563 ms  44.600 ms  44.627 ms
10  210.77.139.150 (210.77.139.150)  53.302 ms  53.233 ms  53.032 ms
11  211.151.104.6 (211.151.104.6)  39.585 ms  39.502 ms  39.598 ms
12  211.151.111.30 (211.151.111.30)  35.161 ms  35.938 ms  36.005 ms
```

Records start with a sequence number from 1, each representing a "hop" or gateway. Each row displays three times in ms, which corresponds to the default parameter of `-q`. After sending three probe packets to each gateway, the gateway's response time is recorded. If you use `traceroute -q 4 www.58.com`, it sends four packets to each gateway.

Sometimes, you may see rows represented by asterisks. This might happen because a firewall is blocking ICMP return messages, preventing any data from being returned.

Sometimes, a long delay at a particular gateway might be due to congestion or hardware issues. DNS problems failing to resolve hostnames can also cause delays; you can add the `-n` parameter to avoid DNS resolution and output results in IP format.

Traceroute can help troubleshoot issues between different network segments in a LAN, determining if a problem lies with a host or a gateway. When experiencing issues accessing a remote server, tracing the route to IDC providers can assist in resolution, though resolving such issues domestically can sometimes be challenging even when the problem location is identified.

**Setting Hops**

```shell
[root@localhost ~]# traceroute -m 10 www.baidu.com
traceroute to www.baidu.com (61.135.169.105), 10 hops max, 40 byte packets
 1  192.168.74.2 (192.168.74.2)  1.534 ms  1.775 ms  1.961 ms
 2  211.151.56.1 (211.151.56.1)  0.508 ms  0.514 ms  0.507 ms
 3  211.151.227.206 (211.151.227.206)  0.571 ms  0.558 ms  0.550 ms
 4  210.77.139.145 (210.77.139.145)  0.708 ms  0.729 ms  0.785 ms
 5  202.106.42.101 (202.106.42.101)  7.978 ms  8.155 ms  8.311 ms
 6  bt-228-037.bta.net.cn (202.106.228.37)  772.460 ms bt-228-025.bta.net.cn (202.106.228.25)  2.152 ms 61.148.154.97 (61.148.154.97)  772.107 ms
 7  124.65.58.221 (124.65.58.221)  4.875 ms 61.148.146.29 (61.148.146.29)  2.124 ms 124.65.58.221 (124.65.58.221)  4.854 ms
 8  123.126.6.198 (123.126.6.198)  2.944 ms 61.148.156.6 (61.148.156.6)  3.505 ms 123.126.6.198 (123.126.6.198)  2.885 ms
 9  * * *
10  * * *
```

Other examples:

```shell
traceroute -m 10 www.baidu.com # Set maximum hops
traceroute -n www.baidu.com    # Display IP addresses, no hostname lookup
traceroute -p 6888 www.baidu.com  # Set the base UDP port for probe packets to 6888
traceroute -q 4 www.baidu.com  # Set the number of probe packets to 4
traceroute -r www.baidu.com    # Bypass normal routing tables, send directly to connected host
traceroute -w 3 www.baidu.com  # Set the wait time for a response to 3 seconds
```
