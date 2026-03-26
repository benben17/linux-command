firewall-cmd
===

Command-line client for firewalld, a dynamic firewall manager similar to iptables.

## Description

`firewall-cmd` is the command-line interface for managing `firewalld`. `firewalld` is a major feature of CentOS 7 (and other modern Linux distributions), offering two primary advantages: it supports dynamic updates without requiring a service restart, and it introduces the concept of firewall "zones."

Compared to `iptables`, `firewalld` offers several benefits:

1. `firewalld` can modify individual rules dynamically without needing to flush and reload the entire rule set.
2. `firewalld` is more user-friendly; most functions can be implemented without a deep understanding of the "five tables and five chains" or the complexities of the TCP/IP protocol.

`firewalld` itself does not perform the firewall filtering; like `iptables`, it uses the kernel's `netfilter` subsystem. Both tools serve to manage rules, while `netfilter` handles the actual packet filtering. They simply differ in structure and usage.

**Command Format**

```shell
firewall-cmd [options ... ]
```

### Options

General Options

```shell
-h, --help    # Display help information.
-V, --version # Display version information. (Cannot be combined with other options).
-q, --quiet   # Do not print status messages.
```

Status Options

```shell
--state                # Display the state of firewalld.
--reload               # Reload firewall rules without interrupting services.
--complete-reload      # Reload firewall rules and interrupt all active connections.
--runtime-to-permanent # Save current runtime rules as permanent.
--check-config         # Check the configuration for correctness.
```

Log Options

```shell
--get-log-denied         # Get the setting for logging denied packets.
--set-log-denied=<value> # Set logging for denied packets. Values: 'all', 'unicast', 'broadcast', 'multicast', 'off'.
```

### Examples

```shell
# Install firewalld
yum install firewalld firewall-config

systemctl start firewalld  # Start service
systemctl stop firewalld   # Stop service
systemctl enable firewalld  # Enable on boot
systemctl disable firewalld # Disable on boot
systemctl status firewalld  # Or use: firewall-cmd --state
```

Switching back to `iptables` (if preferred):

```shell
systemctl stop firewalld
systemctl disable firewalld
yum install iptables-services
systemctl start iptables
systemctl enable iptables
```

Configuring firewalld

```shell
firewall-cmd --version  # View version
firewall-cmd --help     # View help

# View settings:
firewall-cmd --state  # Show state
firewall-cmd --get-active-zones  # View active zones
firewall-cmd --get-zone-of-interface=eth0  # View zone for a specific interface
firewall-cmd --panic-on  # Enable panic mode (reject all packets)
firewall-cmd --panic-off  # Disable panic mode
firewall-cmd --query-panic  # Check if panic mode is enabled

firewall-cmd --reload # Update rules dynamically
firewall-cmd --complete-reload # Full reload (breaks connections)
```

Managing Zones and Interfaces

```shell
# Add an interface to a zone (interfaces are in 'public' by default)
firewall-cmd --zone=public --add-interface=eth0
# To make it permanent, add --permanent and then reload
 
# Set the default zone (takes effect immediately)
firewall-cmd --set-default-zone=public

# View all open ports in a zone:
firewall-cmd --zone=dmz --list-ports

# Add a port to a zone:
firewall-cmd --zone=dmz --add-port=8080/tcp
 
# Add a service (abstracts ports into named services)
firewall-cmd --zone=work --add-service=smtp
 
# Remove a service
firewall-cmd --zone=work --remove-service=smtp

# List all supported zones
firewall-cmd --get-zones

# Set default zone to home
firewall-cmd --set-default-zone=home

# View current active zones
firewall-cmd --get-active-zones

# View all settings for the public zone
firewall-cmd --zone=public --list-all

# Change interface (enp0s3) to internal zone temporarily
firewall-cmd --zone=internal --change-interface=enp03s

# Change interface (enp0s3) to internal zone permanently
firewall-cmd --permanent --zone=internal --change-interface=enp03s
```

Service Management

```shell
# Show available services
firewall-cmd --get-services

# Allow SSH service
firewall-cmd --add-service=ssh

# Remove SSH service
firewall-cmd --remove-service=ssh

# Open TCP port 8080
firewall-cmd --add-port=8080/tcp

# Temporarily allow Samba service for 600 seconds
firewall-cmd --add-service=samba --timeout=600

# List current services in default zone
firewall-cmd --list-services

# Add HTTP service to internal zone permanently
firewall-cmd --permanent --zone=internal --add-service=http
firewall-cmd --reload
```

Port Management

```shell
# Open port 443/TCP
firewall-cmd --add-port=443/tcp

# Permanently open port 3690/TCP
firewall-cmd --permanent --add-port=3690/tcp
firewall-cmd --reload

# List all settings (including added ports)
firewall-cmd --list-all
```

Direct Mode

```shell
# Use direct mode for custom rules (e.g., opening TCP port 9000)
firewall-cmd --direct --add-rule ipv4 filter INPUT 0 -p tcp --dport 9000 -j ACCEPT
firewall-cmd --reload
```

**Custom Service Management**

Options marked with `[P only]` must be used with the `--permanent` flag.

```shell
--new-service=<name>          Create a new custom service [P only]
--new-service-from-file=<file> [--name=<name>]
                               Create a service from a configuration file [P only]
--delete-service=<name>       Delete an existing service [P only]
--info-service=<name>         Display information about a service
--path-service=<name>         Display the path to the service file [P only]
--service=<name> --set-description=<desc>
                               Set a description for the service [P only]
--service=<name> --get-description
                               Get the description for the service [P only]
--service=<name> --set-short=<desc>
                               Set a short description for the service [P only]
--service=<name> --get-short  Get the short description for the service [P only]
                      
--service=<name> --add-port=<portid>[-<portid>]/<protocol>
                               Add a port or port range to the service [P only]
                      
--service=<name> --remove-port=<portid>[-<portid>]/<protocol>
                               Remove a port or port range from the service [P only]
                      
--service=<name> --query-port=<portid>[-<portid>]/<protocol>
                               Check if a port/range is added to the service [P only]
                      
--service=<name> --get-ports  List all ports added to the service [P only]
                      
--service=<name> --add-protocol=<protocol>
                               Add a protocol to the service [P only]
                      
--service=<name> --remove-protocol=<protocol>
                               Remove a protocol from the service [P only]
                      
--service=<name> --query-protocol=<protocol>
                               Check if a protocol is added to the service [P only]
                      
--service=<name> --get-protocols
                               List all protocols added to the service [P only]
```

**Controlling Ports and Services**

Ports can be opened either by port number or by service name. Note that if a service is opened by name, it must be closed by name. If a port is opened by number, it must be closed by number. Always specify the protocol (TCP or UDP).

```shell
firewall-cmd --add-service=mysql        # Open MySQL port
firewall-cmd --remove-service=http      # Block HTTP port
firewall-cmd --list-services            # List open services
firewall-cmd --add-port=3306/tcp        # Open TCP port 3306
firewall-cmd --remove-port=3306/tcp     # Block TCP port 3306
firewall-cmd --add-port=233/udp         # Open UDP port 233
firewall-cmd --list-ports               # List open ports
```

IP Masquerading

```shell
firewall-cmd --query-masquerade # Check if masquerading is enabled
firewall-cmd --add-masquerade   # Enable masquerading
firewall-cmd --remove-masquerade# Disable masquerading
```

**Port Forwarding**

Port forwarding redirects traffic from one address/port to another. If no destination IP is specified, the local machine is used. If an IP is specified without a port, the source port is used.
Ensure that:
1. The target port (e.g., 8080) is open and listening.
2. IP masquerading is enabled.

```shell
# Forward local port 80 traffic to 8080
firewall-cmd --add-forward-port=port=80:proto=tcp:toport=8080
# Forward local port 80 traffic to 192.168.0.1
firewall-cmd --add-forward-port=port=80:proto=tcp:toaddr=192.168.0.1
# Forward local port 80 traffic to 192.168.0.1 on port 8080
firewall-cmd --add-forward-port=port=80:proto=tcp:toaddr=192.168.0.1:toport=8080
```
