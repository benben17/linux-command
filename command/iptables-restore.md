iptables-restore
===

Restore iptables tables from a file.

## Description

The `iptables-restore` command is used to restore IPv4 firewall tables from data specified on STDIN. It is typically used with files created by `iptables-save`.

### Syntax

```shell
iptables-restore [options]
```

### Options

```shell
-c : Restore packet and byte counters.
-t : Specify the name of the table to restore.
```

### Examples

```shell
iptables-restore < iptables.bak
```
