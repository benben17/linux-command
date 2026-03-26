ping
===

Tests network connectivity between hosts (IPv4).

## Description

The **ping command** is used to test the reachability of a host on an Internet Protocol (IP) network. It works by sending ICMP (Internet Control Message Protocol) Echo Request packets to the target host and waiting for an ICMP Echo Reply. This allows you to verify if a remote host is active and measure the round-trip time.

### Syntax

```shell
ping [options] [destination]
```

### Options

```shell
-d: Set the SO_DEBUG socket option.
-c <count>: Stop after sending <count> Echo Request packets.
-f: Flood ping; send packets as fast as they are received or 100 times per second, whichever is more.
-i <interval>: Wait <interval> seconds between sending each packet.
-I <interface>: Use the specified network interface to send packets.
-l <preload>: Send <preload> packets as fast as possible before falling into normal behavior.
-n: Numeric output only; no attempt will be made to resolve symbolic names for host addresses.
-p <pattern>: Fill the packet with the specified hexadecimal pattern.
-q: Quiet output; only display summary statistics at the start and end.
-r: Bypass routing tables and send directly to a host on an attached network.
-R: Record route (IPv4 only).
-s <size>: Specify the number of data bytes to be sent (default is 56, which translates to 64 ICMP data bytes).
-t <ttl>: Set the IP Time to Live.
-v: Verbose output.
-w <deadline>: Exit after <deadline> seconds regardless of how many packets were sent or received.
-W <timeout>: Time to wait for a response, in seconds.
```

### Parameters

Destination: The hostname or IP address of the target host.

### Examples

```shell
[root@localhost ~]# ping www.google.com
PING www.google.com (142.250.190.36) 56(84) bytes of data.
64 bytes from 142.250.190.36: icmp_seq=1 ttl=117 time=14.2 ms
64 bytes from 142.250.190.36: icmp_seq=2 ttl=117 time=13.8 ms
...
--- www.google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 13.842/14.031/14.221/0.189 ms
```
