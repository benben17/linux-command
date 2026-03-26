route
===

Display and set static routing tables in Linux.

## Description

The **route command** is used to display and set the network routing table in the Linux kernel. The routes set by the `route` command are primarily static routes. To achieve communication between two different subnets, a router connecting the two networks or a gateway located in both networks is required.

Setting routes in a Linux system is usually to solve the following problem: if the Linux system is in a local area network (LAN) with a gateway that allows access to the Internet, the IP address of this gateway needs to be set as the default route for the Linux machine. Note that adding a route directly from the command line using the `route` command will not be saved permanently; the route will be lost after the network card or the machine restarts. You can add the `route` command to `/etc/rc.local` to ensure the route setting remains valid permanently.

### Syntax

```shell
route(options)(parameters)
```

### Options

```shell
-A: Sets the address type.
-C: Prints the routing cache of the Linux kernel.
-v: Verbose mode.
-n: Do not perform DNS reverse lookups; display IP addresses directly in numerical form.
-e: Displays the routing table in netstat format.
-net: Routing table to a network.
-host: Routing table to a host.
```

### Parameters

```shell
add: Adds the specified routing record.
del: Deletes the specified routing record.
target: Destination network or host.
gw: Sets the default gateway.
mss: Sets the TCP Maximum Segment Size (MSS) in bytes.
window: Specifies the TCP window size for TCP connections through the routing table.
dev: The network interface represented by the routing record.
```

### Examples

**Display the current routing table:**

```shell
[root@localhost ~]# route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
112.124.12.0    *               255.255.252.0   U     0      0        0 eth1
10.160.0.0      *               255.255.240.0   U     0      0        0 eth0
192.168.0.0     10.160.15.247   255.255.0.0     UG    0      0        0 eth0
172.16.0.0      10.160.15.247   255.240.0.0     UG    0      0        0 eth0
10.0.0.0        10.160.15.247   255.0.0.0       UG    0      0        0 eth0
default         112.124.15.247  0.0.0.0         UG    0      0        0 eth1

[root@localhost ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
112.124.12.0    0.0.0.0         255.255.252.0   U     0      0        0 eth1
10.160.0.0      0.0.0.0         255.255.240.0   U     0      0        0 eth0
192.168.0.0     10.160.15.247   255.255.0.0     UG    0      0        0 eth0
172.16.0.0      10.160.15.247   255.240.0.0     UG    0      0        0 eth0
10.0.0.0        10.160.15.247   255.0.0.0       UG    0      0        0 eth0
0.0.0.0         112.124.15.247  0.0.0.0         UG    0      0        0 eth1
```

The Flags column explains the status of the network node:

*   U (Up): The route is active.
*   H (Host): The destination is a single host.
*   G (Gateway): Use a gateway.
*   R (Reinstate Route): Reinstate route for dynamic routing.
*   D (Dynamically): Dynamically installed by daemon or redirect.
*   M (Modified): Modified from routing daemon or redirect.
*   !: The route is currently closed.

**Add a network route/Set a gateway:**

```shell
route add -net 224.0.0.0 netmask 240.0.0.0 dev eth0    # Add a route to 224.0.0.0.
```

**Block a route:**

```shell
route add -net 224.0.0.0 netmask 240.0.0.0 reject     # Add a blocked route; destination 224.x.x.x will be rejected.
```

**Delete a routing record:**

```shell
route del -net 224.0.0.0 netmask 240.0.0.0
route del -net 224.0.0.0 netmask 240.0.0.0 reject
```

**Delete and add a default gateway:**

```shell
route del default gw 192.168.120.240
route add default gw 192.168.120.240
```
