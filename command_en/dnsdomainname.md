dnsdomainname
===

Display the system's DNS domain name.

## Description

The **dnsdomainname** command is used to show the domain name part of the system's fully qualified domain name (FQDN).

### Syntax

```shell
dnsdomainname (options)
```

### Options

```shell
-v    Verbose mode, output detailed information about the command execution.
```

### Examples

```shell
[root@AY1307311912260196fcZ ~]# dnsdomainname -v
gethostname()=`AY1307311912260196fcZ'
Resolving `AY1307311912260196fcZ' ...
Result: h_name=`AY1307311912260196fcZ'
Result: h_addr_list=`10.160.7.81'
```
