arping
===

Test the network by sending ARP protocol packets

## Additional Information

The **arping command** is a tool used to send ARP requests to an adjacent host. `arping` uses ARP packets to check the hardware address on a device via a mechanism similar to the `ping` command. It can test whether an IP address is already in use on the network and retrieve more device information. Its functionality is similar to `ping`.

### Syntax

```shell
arping (options) (parameters)
```

### Options

```shell
-b: Used to send Ethernet broadcast frames (FFFFFFFFFFFF). arping starts with a broadcast address and uses a unicast address after receiving a response.
-q: Quiet output; do not display any information.
-f: Exit after receiving the first response packet.
-w timeout: Set a timeout in seconds. If the specified time is reached and arping has not fully received a response, it exits.
-c count: Stop after sending the specified number of ARP request packets. If the deadline option is specified, arping waits for the same number of ARP response packets until the timeout occurs.
-s source: Set the value of the SPA field in the ARP packets sent by arping. If empty, it is handled as follows: in DAD mode (Duplicate Address Detection), it is set to 0.0.0.0; in Unsolicited ARP mode (Gratuitous ARP), it is set to the target address; otherwise, it is derived from the routing table.
-I interface: Set the network interface used for pinging.
```

### Parameters

Destination host: Specifies the destination host to which the ARP packets are sent.

### Examples

```shell
[root@localhost ~]# arping www.baidu.com 
ARPING 220.181.111.147 from 173.231.43.132 eth0
Unicast reply from 220.181.111.147 00:D0:03:[bc:48:00]  1.666ms
Unicast reply from 220.181.111.147 [00:D0:03:BC:48:00]  1.677ms
Unicast reply from 220.181.111.147 [00:D0:03:BC:48:00]  1.691ms
Unicast reply from 220.181.111.147 [00:D0:03:BC:48:00]  1.728ms
Unicast reply from 220.181.111.147 [00:D0:03:BC:48:00]  1.626ms
Unicast reply from 220.181.111.147 [00:D0:03:BC:48:00]  1.292ms
Unicast reply from 220.181.111.147 [00:D0:03:BC:48:00]  1.429ms
Unicast reply from 220.181.111.147 [00:D0:03:BC:48:00]  2.042ms
Sent 8 probes (1 broadcast(s))
Received 8 response(s)
```
