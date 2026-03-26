ipcalc
===

A simple IP address calculator.

## Description

The `ipcalc` command is a simple utility for performing IPv4 address calculations. It can calculate broadcast addresses, network addresses, netmasks, and hostnames.

### Syntax

```shell
ipcalc [options]
```

### Options

```shell
-b : Calculate the broadcast address from the given IP address and netmask.
-h : Display the hostname for the given IP address.
-m : Calculate the netmask from the given IP address.
-p : Display the prefix for the given mask or IP address.
-n : Calculate the network address from the given IP address and netmask.
-s : Silent mode; suppress error messages.
--help : Display help information.
```

### Examples

Calculate the prefix:
```shell
[root@localhost ~]# ipcalc -p 192.168.2.1 255.255.255.0
PREFIX=24
```

Calculate the network address:
```shell
[root@localhost ~]# ipcalc -n 192.168.2.1 255.255.255.0
NETWORK=192.168.2.0
```

Get the hostname:
```shell
[root@localhost ~]# ipcalc -h 127.0.0.1
hostname=localhost.localdomain
```

Display multiple fields:
```shell
[root@localhost ~]# ipcalc -pnbm 192.168.2.1 255.255.255.0
NETMASK=255.255.255.0
PREFIX=24
BROADCAST=192.168.2.255
NETWORK=192.168.2.0
```
