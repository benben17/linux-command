named-checkzone
===

Verify and convert zone files

## Description

The **named-checkzone command** is used to check the validity of zone files and convert them. It requires specifying both the zone name and the zone file name.

### Syntax

```shell
named-checkzone [options] [zone_name] [zone_file]
```

### Options

```shell
-q Quiet mode.
-d Enable debugging.
-c <class> Specify the class of the zone. If not specified, IN is used.
```

### Examples

Check the validity of and convert the zone file `/var/named/192.168.0.rev`.

```shell
[root@localhost ~]# named-checkzone 0.168.192.in-addr.arpa /var/named/192.168.0.rev
zone 0.168.192.in-addr.arpa/IN: loaded serial 1268360612
OK
```

Check the validity of and convert the zone file `/var/named/sh.com.hosts`.

```shell
[root@localhost ~]# named-checkzone sh.com /var/named/sh.com.hosts
zone sh.com/IN: sh.com/MX 'mail.sh.com' is a CNAME (illegal)
zone sh.com/IN: loaded serial 1268360234
OK
```
