dhcpd
===

Dynamic Host Configuration Protocol (DHCP) server.

### Syntax

```shell
dhcpd [options] [network_interface]
```

### Options

```shell
-p <port>         Specify the port on which dhcpd listens.
-f                Run dhcpd as a foreground process.
-d                Enable debug mode.
-q                Do not display copyright information on startup.
-t                Test the configuration file for syntax errors only.
-T                Test the lease database file.
-4                Run as a DHCPv4 server.
-6                Run as a DHCPv6 server.
-s <server>       Specify the server to send replies to.
-cf <config_file> Specify the configuration file.
-lf <lease_file>  Specify the lease file.
-pf <pid_file>    Specify the PID file.
-tf <trace_file>  Specify a file to record the entire startup state of the DHCP server.
```

### Examples

Troubleshooting the DHCP server.

```shell
[root@localhost ~]# dhcpd
Internet Systems Consortium DHCP Server 4.1.1-P1
Copyright 2004-2010 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/
Not searching LDAP since ldap-server, ldap-port and ldap-base-dn were not specified in the config file
Wrote 0 deleted host decls to leases file.
Wrote 0 new dynamic host decls to leases file.
Wrote 1 leases to leases file.
Listening on LPF/eth0/00:0c:29:fc:2f:e5/192.168.0.0/24
Sending on   LPF/eth0/00:0c:29:fc:2f:e5/192.168.0.0/24
Sending on   Socket/fallback/fallback-net
[root@rhel ~]# There's already a DHCP server running.
 
This version of ISC DHCP is based on the release available
on ftp.isc.org. Features have been added and other changes
have been made to the base software release in order to make
it work better with this distribution.
 
exiting.
```
