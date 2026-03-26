iptables-save
===

Save iptables table configurations.

## Description

The `iptables-save` command dumps the contents of IPv4 tables to STDOUT in a format that can be read by `iptables-restore`.

### Syntax

```shell
iptables-save [options]
```

### Options

```shell
-c : Include packet and byte counters in the output.
-t : Specify the name of the table to save.
```

### Examples

```shell
iptables-save -t filter > iptables.bak
```
