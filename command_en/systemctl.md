systemctl
===

Control the systemd system and service manager

## Description

The **systemctl command** is a utility for controlling the systemd system and service manager. It essentially combines the functionalities of the older `service` and `chkconfig` commands.

| Task | Old Command | New Command |
| ---- | ---- | ---- |
| Enable a service at boot | chkconfig --level 3 httpd on | systemctl enable httpd.service |
| Disable a service at boot | chkconfig --level 3 httpd off | systemctl disable httpd.service |
| Check service status | service httpd status | systemctl status httpd.service (Detailed) <br> systemctl is-active httpd.service (Active status only) |
| List all enabled services | chkconfig --list | systemctl list-units --type=service |
| Start a service | service httpd start | systemctl start httpd.service |
| Stop a service | service httpd stop | systemctl stop httpd.service |
| Restart a service | service httpd restart | systemctl restart httpd.service |
| Reload a service | service httpd reload | systemctl reload httpd.service |

### Examples

```shell
systemctl start nfs-server.service   # Start NFS service
systemctl enable nfs-server.service  # Enable service at boot
systemctl enable nfs-server.service --now # Enable at boot and start immediately
systemctl disable nfs-server.service # Disable service at boot
systemctl disable nfs-server.service --now # Disable at boot and stop immediately
systemctl status nfs-server.service  # Check current service status
systemctl restart nfs-server.service # Restart a service
systemctl list-units --type=service  # List all active services
```

Open port 22 in the firewall:

```shell
iptables -I INPUT -p tcp --dport 22 -j accept
```

If issues persist, check SELinux:

Disable SELinux:
Change `SELINUX=""` to `disabled` in `/etc/selinux/config` and reboot.

Completely disable firewall:

```shell
sudo systemctl status firewalld.service
sudo systemctl stop firewalld.service          
sudo systemctl disable firewalld.service
```
