arp
===

The arp command is used to display and modify the IP-to-MAC address translation table

## Additional Information

The **arp command** manages the Address Resolution Protocol (ARP), an essential network protocol used to find data link layer addresses by resolving network layer addresses. This command can display and modify the cached data in the ARP resolution table.

This core protocol module implements the Address Resolution Protocol defined in RFC 826, which handles the translation between Layer 2 hardware addresses and IPv4 protocol addresses on directly connected networks. Users typically do not interact with this module directly unless they wish to configure it.

In fact, it provides services to other protocols within the kernel.

User processes can receive ARP packets using `packet(7)` sockets. There is also a mechanism for managing the ARP cache in user space using `netlink(7)` sockets. We can also control the ARP table on any `PF_INET` socket via `ioctl(2)`.

The ARP module maintains a cache of hardware-to-protocol address mappings. This cache has size limits, so infrequent and old entries are cleared by the garbage collector. The garbage collector never deletes entries marked as permanent. We can manipulate the cache directly using `ioctls`, and its behavior can be adjusted using `sysctls` as defined below.

If a positive feedback for an existing mapping is not received within a specified time (see `sysctls` below), the neighbor layer cache record is considered invalid. To send data to the target again, ARP will first attempt to query the local arp process `app_solicit` times to obtain the updated MAC (Media Access Control) address. If it fails and the old MAC address is known, it sends `ucast_solicit` unicast probes. If it still fails, it broadcasts a new ARP request to the network, at which point there should be a queue for data to be sent.

If Linux receives an address request for an address it forwards, and the receiving interface has proxy ARP enabled, Linux will automatically add a non-permanent proxy ARP entry. If a route to the destination is rejected, no proxy ARP entry will be added.

### Syntax

```shell
arp (options) (parameters)
```

### Options

```shell
-a [host]: Display all entries in the ARP cache.
-H [address_type]: Specify the address type used by the arp command.
-d [host]: Delete the ARP entry for the specified host from the ARP cache.
-D: Use the hardware address of the specified interface.
-e: Display entries in the ARP cache using Linux style.
-i [interface]: Specify the network interface to manipulate the ARP cache.
-s [host MAC-address]: Set a static mapping between the specified host's IP address and MAC address.
-n: Display entries in the ARP cache numerically.
-v: Display detailed ARP cache entries, including cache entry statistics.
-f [file]: Set static mappings between host IP addresses and MAC addresses from a file.
```

### Parameters

Host: Query the ARP entry for the specified host in the ARP cache.

### Examples

Display ARP cache contents:

```shell
[root@localhost ~]# arp -v
Address                  HWtype  HWaddress           Flags Mask            Iface
192.168.0.134            ether   00:21:5E:C7:4D:88   C                     eth1
115.238.144.129          ether   38:22:D6:2F:B2:F1   C                     eth0
Entries: 2      Skipped: 0      Found: 2
```

Add a static ARP mapping:

```shell
arp -s IP MAC-ADDRESS
arp -s 192.168.1.1 00:b1:b2:b3:b4:b5
```

Delete an ARP cache entry:

```shell
arp -d 192.168.1.1
```
