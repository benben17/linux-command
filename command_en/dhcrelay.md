dhcrelay
===

Relay DHCP and BOOTP requests.

## Description

The **dhcrelay** command provides a means for relaying DHCP and BOOTP requests from a subnet without a DHCP server to one or more DHCP servers on other subnets. This command is used on a DHCP relay server and supports both DHCPv4/BOOTP and DHCPv6 protocols.

### Syntax

```shell
dhcrelay [options] [DHCP_server]
```

### Options

```shell
-c <hops>    Maximum number of hops for a packet to traverse. The default is 10, maximum is 255.
-4           Run as a DHCPv4/BOOTP relay agent. This is the default mode.
-6           Run as a DHCPv6 relay agent.
-q           Quiet mode.
-p <port>    Listen and send port. The default for DHCPv4/BOOTP is 67, for DHCPv6 is 547.
-A <length>  Specify the maximum packet size sent to the DHCP server.
-d           Force dhcrelay to run as a foreground process.
```

### Examples

Specify the location of the DHCP server.

```shell
[root@localhost ~]# dhcrelay 192.168.0.2
Internet Systems Consortium DHCP Relay Agent 4.1.1-P1
Copyright 2004-2010 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/
Listening on LPF/eth1/00:0c:29:fc:2f:ef
Sending on   LPF/eth1/00:0c:29:fc:2f:ef
Listening on LPF/eth0/00:0c:27:fc:25:ec
Sending on   LPF/eth0/00:0c:27:fc:25:ec
Sending on   Socket/fallback
```
