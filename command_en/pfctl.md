pfctl
===

The configuration command for the PF firewall.

## Description

The **pfctl command** is the control utility for the Packet Filter (PF) firewall. PF is a software system used for TCP/IP traffic filtering and Network Address Translation (NAT) on Unix-like systems. It also provides traffic shaping, bandwidth control, and packet prioritization. PF was originally developed by Daniel Hartmeier and is now maintained by the OpenBSD team.

### Activation

To activate PF and have it load its configuration at boot, edit `/etc/rc.conf` and set:

```shell
pf=yes
```

You can also start and stop PF manually using `pfctl`:

```shell
pfctl -e  # Enable PF
pfctl -d  # Disable PF
```

Note that enabling PF does not automatically load rules unless they were loaded at boot or are loaded manually.

### Configuration

PF loads its rules from `/etc/pf.conf` by default. The file is divided into seven main sections:

1.  **Macros:** User-defined variables (e.g., IP addresses, interface names).
2.  **Tables:** Structures to hold lists of IP addresses.
3.  **Options:** Variables that control how PF operates.
4.  **Scrubbing:** Normalizing packets (e.g., defragmentation).
5.  **Queuing:** Bandwidth control and prioritization.
6.  **Translation (NAT):** Network Address Translation and redirection.
7.  **Filter Rules:** Selective filtering and blocking of packets.

These sections should appear in this order in the configuration file.

### Control

After boot, PF can be managed using `pfctl`. Examples:

```shell
pfctl -f /etc/pf.conf   # Load the pf.conf file
pfctl -nf /etc/pf.conf  # Parse the file without loading it
pfctl -sn               # Show current NAT rules
pfctl -sr               # Show current filter rules
pfctl -ss               # Show current state table
pfctl -si               # Show filter statistics and counters
pfctl -sa               # Show all available information
```

For a full list of commands, refer to the `pfctl` man page.
