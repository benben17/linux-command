ethtool
===

Display or modify Ethernet card configurations.

## Description

The **ethtool** command is used to retrieve or change the configuration of Ethernet network interfaces. It is a complex command with a wide range of features.

### Syntax

```shell
ethtool [ -a | -c | -g | -i | -d | -k | -r | -S |] ethX
ethtool [-A] ethX [autoneg on|off] [rx on|off] [tx on|off]
ethtool [-C] ethX [adaptive-rx on|off] [adaptive-tx on|off] [rx-usecs N] [rx-frames N] [rx-usecs-irq N] [rx-frames-irq N] [tx-usecs N] [tx-frames N] [tx-usecs-irq N] [tx-frames-irq N] [stats-block-usecs N][pkt-rate-low N][rx-usecs-low N] [rx-frames-low N] [tx-usecs-low N] [tx-frames-lowN] [pkt-rate-high N] [rx-usecs-high N] [rx-frames-high N] [tx-usecs-high N] [tx-frames-high N] [sample-interval N]
ethtool [-G] ethX [rx N] [rx-mini N] [rx-jumbo N] [tx N]
ethtool [-e] ethX [raw on|off] [offset N] [length N]
ethtool [-E] ethX [magic N] [offset N] [value N]
ethtool [-K] ethX [rx on|off] [tx on|off] [sg on|off] [tso on|off]
ethtool [-p] ethX [N]
ethtool [-t] ethX [offline|online]
ethtool [-s] ethX [speed 10|100|1000] [duplex half|full] [autoneg on|off] [port tp|aui|bnc|mii] [phyad N] [xcvr internal|external]
[wol p|u|m|b|a|g|s|d...] [sopass xx:yy:zz:aa:bb:cc] [msglvl N]
```

### Options

```shell
-a: Display the status of RX, TX, and Autonegotiate modules (on/off).
-A: Modify the status of RX, TX, and Autonegotiate modules.
-c: Display the Coalesce information of the specified Ethernet card.
-C: Change the Coalesce setting of the specified Ethernet card.
-g: Display the RX/TX ring parameter information.
-G: Change the RX/TX ring setting.
-i: Display driver information (name, version, etc.).
-d: Display register dump information (some drivers may not support this).
-e: Display EEPROM dump information (some drivers may not support this).
-E: Modify Ethernet card EEPROM bytes.
-k: Display the status of Offload parameters (on/off), including RX checksumming, TX checksumming, etc.
-K: Modify Offload parameter status.
-p: Identify the physical location of the NIC by flashing the LED on the port. N indicates the duration in seconds.
-r: Restart auto-negotiation if the module is enabled.
-S: Display NIC- and driver-specific statistics (bytes sent/received, broadcast packets, etc.).
-t: Execute a self-test (offline or online modes).
-s: Modify various NIC settings, including speed, duplex mode, MAC address, etc.
```

### Data Sources

The information displayed by `ethtool` comes from the network driver layer (the data link layer of the TCP/IP stack). The logic in the Linux kernel is implemented as follows:

The most important structure is `struct ethtool_ops`. Its members are function pointers used to display or modify Ethernet configurations (see the second column in the table below).

The NIC driver is responsible for implementing (some of) these functions and wrapping them into the `ethtool_ops` structure, providing a unified interface for the network core. Therefore, different drivers may return different information. The relationship between command options, `ethtool_ops` members, and data sources is shown below:

| Option | struct ethtool\_ops Member | Source of Parameters (e.g., BNX2 driver) |
| ----- | ----- | ----- |
| (None) -s | get\_settings, get\_wol, get\_msglevel, get\_link, set\_settings, set\_wol, set\_msglevel | Retrieves speed and other info from NIC registers; configurable. |
| -a -A | get\_pauseparam, set\_pauseparam | Retrieves Autonegotiate/RX/TX module status from registers; configurable. |
| -c -C | get\_coalesce, set\_coalesce | Retrieves coalescing parameters from registers: delay time/packet count for TX/RX interrupts. Reducing these can improve response time. Setting to 0 stops interrupts. |
| -g -G | get\_ringparam, set\_ringparam | Current TX/RX ring values from registers (configurable); others are driver-fixed. |
| -k -K | get\_rx\_csum, get\_tx\_csum, get\_sg, get\_tso, set\_rx\_csum, set\_tx\_csum, set\_sg, set\_tso | Read from variables storing the state; no corresponding registers. Checksumming modules are often always 'on' and cannot be modified. |
| -i | get\_drvinfo | Fixed driver information: driver name, version, firmware, bus info. |
| -d | get\_drvinfo, get\_regs | Not supported if `get_regs` is not implemented in the driver. |
| -e -E | get\_eeprom, set\_eeprom | Not supported if `get_eeprom` is not implemented in the driver. |
| -r | nway\_reset | Configures the MII\_BMCR register to restart Auto-negotiation. |
| -p | phys\_id | Configures the LED register to flash the LED. |
| -t | self\_test | Tests hardware modules (registers, memory, loopback, link, interrupts) via registers. |
| -S | get\_ethtool\_stats | Statistics from the `stats_blk` structure in the driver (NIC uses DMA to read statistics registers into this structure). Refer to the chip manual for specific meanings. |

As shown above, `ethtool` is primarily used to display or configure hardware (registers) through the driver.

### Examples

Check the speed of a network card:

```shell
ethtool eth0
```

The `Speed:` field in the output indicates the speed. To disable the TX module:

```shell
ethtool -A tx off eth0
```

Verify with `ethtool -a eth0`. To check the driver of `eth0`:

```shell
ethtool -i eth0
```

Disable RX checksumming:

```shell
ethtool -K eth0 rx off
```

Identify the physical port of `eth0` (flashes for 10 seconds):

```shell
ethtool -p eth0 10
```

View detailed statistics:

```shell
ethtool -S eth0
```

Reduce the speed of a Gigabit card to 100Mbps:

```shell
ethtool -s eth0 speed 100
```
