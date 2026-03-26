mii-tool
===

Configure and view media-independent interface (MII) status

## Description

The **mii-tool command** is used to view and manage the status of a network interface's media-independent interface (MII) unit. It is often used to configure the negotiation mode of a network card, such as 10/100/1000 Mbps speeds and half-duplex, full-duplex, or auto-negotiation settings. While most modern network devices use auto-negotiation by default, `mii-tool` is useful when auto-negotiation fails or when specific settings are required to reduce packet loss.

### Syntax

```shell
usage: mii-tool [-VvRrwl] [-A media,... | -F media] [interface ...]
```

### Options

```shell
-V      Display version information.
-v      Display detailed information about network interfaces.
-R      Reset MII to its power-on state.
-r      Restart auto-negotiation.
-w      Watch for link status changes.
-l      Log events to the system log.
-A      Advertise only the specified media types.
-F      Force a specific media mode.

media: 100baseT4, 100baseTx-FD, 100baseTx-HD, 10baseT-FD, 10baseT-HD,
       (to advertise both HD and FD) 100baseTx, 10baseT
```

### Examples

View the negotiation status of a network interface:

```shell
[root@localhost ~]# mii-tool -v eth0
eth0: negotiated 100baseTx-FD, link ok
  product info: vendor 00:50:ef, model 60 rev 8
  basic mode:   autonegotiation enabled
  basic status: autonegotiation complete, link ok
  capabilities: 100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD
  advertising:  100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD flow-control
  link partner: 100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD
```

Force the negotiation mode of a network interface:

Use the `-F` option followed by the desired mode (e.g., 100baseTx-FD):

```shell
[root@localhost ~]# mii-tool -F 100baseTx-FD eth0
[root@localhost ~]# mii-tool -v eth0
eth0: 100 Mbit, full duplex, link ok
  product info: vendor 00:00:00, model 0 rev 0
  basic mode:   100 Mbit, full duplex
  basic status: link ok
  capabilities: 100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD
  advertising:  100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD
```

Note: You can also use the `ethtool` utility for similar purposes, for example:

```shell
[root@localhost ~]# ethtool -s eth0 speed 100 duplex full
```
