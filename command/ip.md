ip
===

Display or manipulate routing, network devices, interfaces, and tunnels.

## Description

The `ip` command is a powerful tool for network configuration on Linux. It replaces older utilities like `ifconfig` and `route` and provides more comprehensive management of the network stack.

### Syntax

```shell
ip [OPTIONS] OBJECT { COMMAND | help }
ip [ -force ] -batch filename
```

### Objects

```shell
OBJECT := { link | address | addrlabel | route | rule | neigh | ntable |
       tunnel | tuntap | maddress | mroute | mrule | monitor | xfrm |
       netns | l2tp | macsec | tcp_metrics | token }
```

### Options

```shell
-V : Print version information.
-s : Print more detailed statistics.
-f : Force the use of a specific protocol family (inet, inet6, etc.).
-4 : Use IPv4.
-6 : Use IPv6.
-0 : Output each record on a single line.
-r : Resolve IP addresses to hostnames.
-h : Print human-readable statistics.
-o : Output each record on a single line (useful for scripting).
```

### Examples

**Manage Interfaces:**
```shell
ip link show                    # Show network interface information
ip link set eth0 up             # Activate an interface
ip link set eth0 down           # Deactivate an interface
ip link set eth0 promisc on     # Enable promiscuous mode
ip link set eth0 mtu 1400       # Set MTU
```

**Manage IP Addresses:**
```shell
ip addr show                    # Show IP address information
ip addr add 192.168.0.1/24 dev eth0 # Add an IP address
ip addr del 192.168.0.1/24 dev eth0 # Delete an IP address
```

**Manage Routing:**
```shell
ip route show                   # Show the routing table
ip route add default via 192.168.1.254 # Add a default gateway
ip route add 192.168.4.0/24 via 192.168.0.254 dev eth0 # Add a static route
ip route del 192.168.4.0/24     # Delete a route
```

**Show Detailed Statistics:**
```shell
ip -s link list
```

**Show Neighbors (ARP table):**
```shell
ip neigh list
```

**Get All Interface Names:**
```shell
ip link | grep -E '^[0-9]' | awk -F: '{print $2}'
```
