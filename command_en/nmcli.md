nmcli
===

Command-line tool for controlling NetworkManager

## Description

The **nmcli command** is the command-line interface for NetworkManager, used to create, display, edit, delete, activate, and deactivate network connections, as well as to control and display network device status.

### Syntax

```shell
nmcli [OPTIONS] OBJECT { COMMAND | help }
```

### Options

```shell
OPTIONS
  -t[erse]                                  # Terse output (minimalistic).
  -p[retty]                                 # Pretty output (human-friendly).
  -m[ode] tabular|multiline                 # Output mode.
  -f[ields] <field1,field2,...>|all|common  # Specify fields to output.
  -e[scape] yes|no                          # Escape column separators in values.
  -n[ocheck]                                # Do not check nmcli and NetworkManager versions.
  -a[sk]                                    # Ask for missing parameters.
  -w[ait] <seconds>                         # Set timeout for waiting for operation completion.
  -v[ersion]                                # Show version.
  -h[elp]                                   # Print help.

OBJECT
  g[eneral]       General status and operations of NetworkManager.
  n[etworking]    Overall networking control.
  r[adio]         NetworkManager radio switches (Wi-Fi, WWAN).
  c[onnection]    NetworkManager's connections.
  d[evice]        Devices managed by NetworkManager.
  a[gent]         NetworkManager secret agent or polkit agent.
```

### Examples

```shell
nmcli connection show            # View current connection status
nmcli connection reload          # Reload connection profiles from disk
nmcli connection show -active    # List active connections
nmcli connection show "lan eth0" # Show details for a specific connection
nmcli device status              # Show status of devices
nmcli device show eno16777736    # Show properties of a specific interface
nmcli device show                # Show properties of all interfaces
nmcli con up static              # Activate the "static" connection profile
nmcli con up default             # Activate the "default" connection profile
nmcli con add help               # View help for adding connections
```

### Creating a Network Session

```shell
nmcli connection add con-name company ifname ens33 autoconnect no type ethernet ip4 192.168.1.2/24 gw4 192.168.1.1
# con-name: Specifies the connection profile name.
# ifname: Specifies the network interface.
# autoconnect no: Do not connect automatically.
# type ethernet: Specifies the connection type.
# ip4/ip6: IPv4 or IPv6 address.
# gw4/gw6: Gateway address.
```
