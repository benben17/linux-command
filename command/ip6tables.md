ip6tables
===

IPv6 packet filter administration.

## Description

The `ip6tables` command is used to set up, maintain, and inspect the tables of IPv6 packet filter rules in the Linux kernel. It is the IPv6 equivalent of `iptables`.

### Syntax

```shell
ip6tables [options]
```

### Options

```shell
-t <table> : Specify the table to operate on (default is 'filter').
-A : Append one or more rules to the end of the selected chain.
-D : Delete one or more rules from the selected chain.
-I : Insert one or more rules in the selected chain as the given rule number.
-R : Replace a rule in the selected chain.
-L : List all rules in the selected chain.
-F : Flush the selected chain (delete all rules).
-Z : Zero the packet and byte counters in all chains.
-N : Create a new user-defined chain.
-P : Set the policy for the chain to the given target.
-h : Display help information.
-p : Specify the protocol of the rule or the packet to check.
-s : Specify the source address.
-j <target> : Specify the target of the rule (what to do if the packet matches).
-i <interface> : Name of an interface via which a packet was received.
-o <interface> : Name of an interface via which a packet is going to be sent.
-c <counters> : Initialize packet and byte counters during insert, append, or replace operations.
```

### Examples

View the current IPv6 firewall configuration:

```shell
ip6tables -nL --line-numbers
```

#### Edit `/etc/sysconfig/ip6tables`

Open the file with an editor:

```shell
vi /etc/sysconfig/ip6tables
```

Example rules:

```shell
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:RH-Firewall-1-INPUT - [0:0]
-A INPUT -j RH-Firewall-1-INPUT
-A FORWARD -j RH-Firewall-1-INPUT
-A RH-Firewall-1-INPUT -i lo -j ACCEPT
-A RH-Firewall-1-INPUT -p icmpv6 -j ACCEPT
-A RH-Firewall-1-INPUT -m tcp -p tcp --dport 22 -j ACCEPT
-A RH-Firewall-1-INPUT -j REJECT --reject-with icmp6-adm-prohibited
COMMIT
```

To open port 80 (HTTP), add this before the COMMIT line:

```shell
-A RH-Firewall-1-INPUT -m tcp -p tcp --dport 80 -j ACCEPT
```

To open port 53 (DNS) for both TCP and UDP:

```shell
-A RH-Firewall-1-INPUT -m tcp -p tcp --dport 53 -j ACCEPT
-A RH-Firewall-1-INPUT -m udp -p udp --dport 53 -j ACCEPT
```

To log and drop packets that don't match any rules:

```shell
-A RH-Firewall-1-INPUT -j LOG
-A RH-Firewall-1-INPUT -j DROP
COMMIT
```

Restart the service:

```shell
# service ip6tables restart
```

#### Allow Specific ICMPv6 Traffic

IPv6 requires more ICMP types to function correctly (e.g., for Neighbor Discovery).

```shell
-A INPUT -p icmpv6 -j ICMPv6
-A ICMPv6 -p icmpv6 --icmpv6-type echo-request -j ACCEPT
-A ICMPv6 -p icmpv6 --icmpv6-type destination-unreachable -j ACCEPT
-A ICMPv6 -p icmpv6 --icmpv6-type packet-too-big -j ACCEPT
-A ICMPv6 -p icmpv6 --icmpv6-type time-exceeded -j ACCEPT
-A ICMPv6 -p icmpv6 --icmpv6-type parameter-problem -j ACCEPT
-A ICMPv6 -p icmpv6 --icmpv6-type router-solicitation -j ACCEPT
-A ICMPv6 -p icmpv6 --icmpv6-type router-advertisement -j ACCEPT
-A ICMPv6 -p icmpv6 --icmpv6-type neighbour-solicitation -j ACCEPT
-A ICMPv6 -p icmpv6 --icmpv6-type neighbour-advertisement -j ACCEPT
-A ICMPv6 -j RETURN
-A OUTPUT -p icmpv6 -j ACCEPT
```
