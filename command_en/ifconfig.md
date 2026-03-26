ifconfig
===

Configure and display network interface parameters for Linux systems.

## Description

The `ifconfig` command is used to configure or display network interface parameters for the Linux kernel. Changes made with `ifconfig` are not persistent across reboots or interface restarts. To make permanent changes, you must edit the network configuration files.

### Syntax

```shell
ifconfig [interface] [options] [address]
```

### Parameters

```shell
add <address> : Set an IPv6 address for the network interface.
del <address> : Remove an IPv6 address from the network interface.
down : Deactivate the specified network interface.
hw <type> <address> : Set the hardware type and address (MAC) of the interface.
io_addr <address> : Set the I/O address for the network interface.
irq <address> : Set the IRQ for the network interface.
media <type> : Set the media type for the network interface.
mem_start <address> : Set the start address of the memory used by the interface.
metric <number> : Set the routing metric.
mtu <bytes> : Set the Maximum Transmission Unit (MTU) for the interface.
netmask <mask> : Set the subnet mask for the interface.
tunnel <address> : Create a tunnel address between IPv4 and IPv6.
up : Activate the specified network interface.
-broadcast <address> : Treat packets to this address as broadcast packets.
-pointopoint <address> : Establish a direct connection with another interface.
-promisc : Enable or disable promiscuous mode for the interface.
IP address : Specify the IP address for the interface.
interface : Specify the name of the network interface.
```

### Examples

**Display active network interface information:**

```shell
[root@localhost ~]# ifconfig
eth0      Link encap:Ethernet  HWaddr 00:16:3E:00:1E:51  
          inet addr:10.160.7.81  Bcast:10.160.15.255  Mask:255.255.240.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:61430830 errors:0 dropped:0 overruns:0 frame:0
          TX packets:88534 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:3607197869 (3.3 GiB)  TX bytes:6115042 (5.8 MiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:56103 errors:0 dropped:0 overruns:0 frame:0
          TX packets:56103 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:5079451 (4.8 MiB)  TX bytes:5079451 (4.8 MiB)
```

Explanation:

- **eth0**: Represents the first network card. `HWaddr` is the physical (MAC) address, here `00:16:3E:00:1E:51`.
- **inet addr**: The IP address of the card, here `10.160.7.81`. `Bcast` is the broadcast address, and `Mask` is the subnet mask.
- **lo**: The loopback address, typically `127.0.0.1`. Used for testing network software locally.
- **Line 1**: Connection type (Ethernet) and MAC address.
- **Line 2**: IP address, broadcast address, and subnet mask.
- **Line 3**: `UP` (interface is active), `RUNNING` (cable connected), `MULTICAST` (supports multicast), `MTU` (Maximum Transmission Unit).
- **Lines 4-5**: Statistics for received (RX) and transmitted (TX) packets.
- **Line 7**: Statistics for received and transmitted bytes.

**Activate or deactivate a network interface:**

```shell
ifconfig eth0 up
ifconfig eth0 down
```
*Be careful when disabling interfaces via SSH; you may lose connection.*

**Add or remove an IPv6 address:**

```shell
ifconfig eth0 add 33ffe:3240:800:1005::2/64
ifconfig eth0 del 33ffe:3240:800:1005::2/64
```

**Change the MAC address:**

```shell
ifconfig eth0 hw ether 00:AA:BB:CC:dd:EE
```

**Configure an IP address:**

```shell
ifconfig eth0 192.168.2.10
ifconfig eth0 192.168.2.10 netmask 255.255.255.0
ifconfig eth0 192.168.2.10 netmask 255.255.255.0 broadcast 192.168.2.255
```

**Enable or disable ARP:**

```shell
ifconfig eth0 arp
ifconfig eth0 -arp
```

**Set MTU:**

```shell
ifconfig eth0 mtu 1500
```

**Other examples:**

```shell
ifconfig       # Display active interfaces
ifconfig -a    # Display all interfaces, including inactive ones
ifconfig eth0  # Display info for eth0 only
```
