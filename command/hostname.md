hostname
===

Show or set the system's host name.

## Supplemental Information

The **hostname command** is used to display or set the system's host name.

- The `HOSTNAME` environment variable also stores the current host name.
- When using the `hostname` command to set the host name, the change is not permanent and will be lost after a reboot. To make the change permanent, you must modify `/etc/hosts` and `/etc/sysconfig/network` (or `/etc/hostname` on modern systems) and reboot. Alternatively, use the `hostnamectl` command for permanent changes.

### Syntax

```shell
hostname [-b] {hostname|-F file}           # Set host name (or get from file)
hostname [-a|-A|-d|-f|-i|-I|-s|-y]         # Show formatted name
hostname                                   # Show host name

{yp,nis,}domainname {nisdomain|-F file}    # Set NIS domain name (or get from file)
{yp,nis,}domainname                        # Show NIS domain name

dnsdomainname                              # Show DNS domain name

hostname -V|--version|-h|--help            # Print info and exit
```

### Options

```shell
-a, --alias               # Show host aliases
-A, --all-fqdns           # Show all FQDNs
-b, --boot                # Set default hostname if none is available
-d, --domain              # Show DNS domain name
-f, --fqdn, --long        # Show FQDN (Fully Qualified Domain Name)
-F, --file                # Read host name or NIS domain name from the specified file
-i, --ip-address          # Show the IP address(es) of the host name
-I, --all-ip-addresses    # Show all network addresses of the host
-s, --short               # Show short host name (truncated at the first dot)
-y, --yp, --nis           # Show NIS domain name
```

### Examples

Display the host name:
```shell
[root@AY1307311912260196fcZ ~]# hostname
AY1307311912260196fcZ
```

Temporarily change the host name:
```shell
[root@AY1307311912260196fcZ ~]# hostname newname
```

Display all IP addresses of the host:
```shell
[root@AY1307311912260196fcZ ~]# hostname -I
10.17.0.1 10.18.0.10 172.17.0.1
```
