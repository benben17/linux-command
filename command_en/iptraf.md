iptraf
===

Real-time network statistics viewer.

## Description

The `iptraf` command is an ncurses-based IP LAN monitor that generates various network statistics including TCP info, UDP counts, ICMP and OSPF information, Ethernet load info, node stats, IP checksum errors, and others.

### Syntax

```shell
iptraf [options]
```

### Options

```shell
-i interface : Start the IP traffic monitor on a specific interface immediately.
-g : Start the general interface statistics immediately.
-d interface : Start the detailed statistics on a specific interface immediately.
-s interface : Start the TCP and UDP monitor on a specific interface immediately.
-z interface : Show packet counts for a specific interface.
-l interface : Start the LAN station monitor on a specific interface immediately.
-t timeout : Specify the length of time iptraf should run.
-B : Run the program in the background (redirects output to /dev/null).
-f : Clear all counters.
-h : Display help information.
```
