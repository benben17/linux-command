ping6
===

Tests network connectivity between hosts (IPv6).

## Description

The **ping6 command** is the IPv6 version of the `ping` utility. It uses ICMPv6 to send Echo Request messages and receive Echo Replies to verify if an IPv6 destination is reachable. To use it successfully, your local environment must be configured for IPv6.

### Syntax

```bash
ping6 [options] [destination] [interface]
```

### Options

```bash
-a [addrtype]: Generate ICMPv6 Node Information Node Address Queries.
-b [bufsiz]: Set the socket buffer size.
-c [count]: Stop after sending (and receiving) <count> ECHO_RESPONSE packets.
-h [hoplimit]: Set the IPv6 hop limit.
-I [interface]: Send packets via the specified interface.
-i [wait]: Wait <wait> seconds between sending each packet (default is 1 second).
-p [policy]: Specify an IPsec policy for the probe.
```

### Parameters

Destination: The IPv6 address or hostname of the target host.

### Examples

```bash
$ ping6 -c4 ipw.cn

PING6(56=40+8+8 bytes) 2409:xxxx:xxxx:85c0::2 --> 2409:8c70:3a00:42:3a::1
16 bytes from 2409:8c70:3a00:42:3a::1, icmp_seq=0 hlim=54 time=31.236 ms
...
--- ipw.cn ping6 statistics ---
4 packets transmitted, 4 packets received, 0.0% packet loss
round-trip min/avg/max/std-dev = 28.973/29.791/31.236/0.862 ms
```

### Common Reasons for IPv6 Ping Failure

1.  IPv6 is not enabled on the server.
2.  The firewall or security group does not allow ICMPv6 traffic from the source address (e.g., `::/0`).
