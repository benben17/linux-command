nslookup
===

Query Internet name servers interactively

## Description

The **nslookup command** is a network administration tool for querying the Domain Name System (DNS) to obtain domain name or IP address mapping or other DNS records.

`nslookup` has two modes: "interactive" and "non-interactive". In "interactive mode", the user can query name servers for information about various hosts and domains or to print a list of hosts in a domain.

In "non-interactive mode", the user can retrieve specific information for a single host or domain. You can also specify the DNS server to use for the query.

To enter interactive mode, run `nslookup` without arguments. It will connect to the default DNS server listed in `/etc/resolv.conf`. Alternatively, you can run `nslookup - [nameserver]`. For non-interactive mode, simply use `nslookup [domain]`.

### Syntax

```shell
nslookup [options] [domain] [dns_server]
```

### Options

```shell
-sil: Suppress warning messages.
```

### Parameters

Domain: Specifies the domain name to query.

### DNS Server
If not specified, the default server from `/etc/resolv.conf` is used. If a DNS server IP is provided, `nslookup` will query that specific server.

### Examples

```shell
[root@localhost ~]# nslookup www.jsdig.com
Server:         202.96.104.15
Address:        202.96.104.15#53

Non-authoritative answer:
www.jsdig.com canonical name = host.1.jsdig.com.
Name:   host.1.jsdig.com
Address: 100.42.212.8

[root@localhost ~]# nslookup www.sustech.edu.cn 8.8.8.8
Server:		8.8.8.8
Address:	8.8.8.8#53

Non-authoritative answer:
www.sustech.edu.cn	canonical name = www.sustech.edu.cn.w.cdngslb.com.
Name:	www.sustech.edu.cn.w.cdngslb.com
Address: 113.96.179.222
```
