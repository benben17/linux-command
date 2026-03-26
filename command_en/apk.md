apk
===

The package management tool for Alpine Linux.


## Usage Examples

```shell
apk add xxx           # Install a package
apk search xxx        # Search for a package (supports regex)
apk info xxx          # View detailed information about a package
apk show              # List local packages
apk del openssh openntp vim  # Uninstall and remove packages
```

### Upgrade

The `upgrade` command upgrades all installed packages in the system (typically including the kernel). You can also specify certain packages to be upgraded only.

```shell
apk update            # Update the local index of available packages
apk upgrade           # Upgrade all installed packages
apk add --upgrade busybox  # Upgrade a specific package
```

### Search

```shell
apk search            # Search for all available packages
apk search -v         # Search for available packages and their descriptions
apk search -v 'acf*'  # Search for packages by name
apk search -v -d 'docker'  # Search for packages by their descriptions
```

### View Package Information

The `info` command is used to display information about packages.

```shell
apk info              # List all installed packages
apk info -a zlib      # Show complete package information for 'zlib'
apk info --who-owns /sbin/lbu  # Show which package a specific file belongs to
```


## Notes

Alpine is quite nice—simple and pure.

```shell
apk add iproute2      # Provides 'ss' command (modern alternative to netstat)
ss -ptl
apk add drill         # Modern alternative to nslookup & dig

crond                 # Start the cron service
crontab -l -e         # List or edit cron jobs

apk add xxx
apk search -v xxx
apk info -a xxx
apk info

# Change repositories (example for Aliyun mirrors)
echo -e "http://mirrors.aliyun.com/alpine/v3.6/main\nhttp://mirrors.aliyun.com/alpine/v3.6/community" > /etc/apk/repositories
apk update

# Storage
lbu                   # Alpine Local Backup tool

# Network
echo "shortname" > /etc/hostname
hostname -F /etc/hostname
/etc/hosts
/etc/resolv.conf      # Configure DNS
modprobe ipv6         # Enable IPv6
echo "ipv6" >> /etc/modules
iface                 # Configure interfaces (check /etc/network/interfaces)
apk add iptables ip6tables iptables-doc
/etc/init.d/networking restart  # Activate network changes

apk add iputils       # Provides IPv6 traceroute
traceroute6 ipv6.google.com
awall                 # Alpine Wall (firewall manager)

# Post-install & Advanced usage
/etc/apk/repositories
# Install from a specific repository
apk add cherokee --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted

apk search -v --description 'NTP'  # Search descriptions
apk info -a zlib
apk info -vv | sort
apk info -r -R        # Show reverse dependencies / requirements
apk version -v -l '<' # Show available updates
apk upgrade -U -a     # Upgrade with repository update
apk add -u xxx        # Update specific package

# Runlevels & Services
/etc/runlevels        # View runlevels
apk add openrc        # Install OpenRC init system
rc-update add xxx boot # Set service to start at boot
rc-service xxx start  # Start a service (same as /etc/init.d/xxx start)
rc-status             # Check status of services

# User management
adduser xxx
passwd xxx

# Configuration Management (Ansible example)
apk add ansible       # Server side
ssh-keygen
/etc/ansible/hosts
apk add python        # Node side
ssh-copy-id

# Documentation & Shell
apk add man man-pages mdocml-apropos less less-doc
export PAGER=less
apk add bash bash-doc bash-completion  # Install Bash

# Core utilities
apk add util-linux pciutils usbutils coreutils binutils findutils grep

# Development & Compilation
apk add build-base gcc abuild binutils binutils-doc gcc-doc
apk add cmake cmake-doc extra-cmake-modules extra-cmake-modules-doc
apk add ccache ccache-doc

# Docker
apk add docker
rc-update add docker boot
rc-service docker start
apk add py-pip
pip install docker-compose
ln -s /usr/bin/docker-compose /usr/bin/doc

# Applications
apk add openssh       # SSH server/client
rc-update add sshd
/etc/init.d/sshd start
/etc/sshd_config
apk add dropbear      # Alternative lightweight SSH implementation
```
