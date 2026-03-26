iscsiadm
===

iscsi administration tool.

## Description

The `iscsiadm` command is used to manage iSCSI (Internet Small Computer System Interface) connections. iSCSI is a network-based storage protocol that allows block-level data transfer between computers. `iscsiadm` provides functionality to discover, configure, and manage iSCSI storage devices.

```shell
sudo yum install iscsi-initiator-utils   # Install iscsiadm (CentOS/RHEL)
/etc/iscsi/initiatorname.iscsi           # Initiator name configuration file
sudo systemctl enable iscsi              # Enable service at boot
sudo systemctl enable iscsid             
sudo systemctl restart iscsi             # Restart service
sudo systemctl restart iscsid           
```

### Syntax

```shell
iscsiadm [options] <command> <parameters>
```

### Options

```shell
-m, --mode         # Specify the mode: discovery, node, session, discoverydb, host, or iface.
-t, --type         # Specify type (e.g., sendtargets or st, isns, fw), used only in discovery mode.
-T, --targetname   # Specify target name, used only in node mode.
-p, --portal       # <ip:port> Specify target IP (default port 3260), used in discovery and node modes.
-l, --login        # Log in to an iSCSI device.
-u, --logout       # Log out of an iSCSI device.
-I, --interface    # Specify network interface for iSCSI operations.
-P, --print        # <0-4> Print level of detail.
-s, --stats        # View session statistics.
-h, --help         # Display help.
-V, --version      # Display version information.
```

### Examples

**Discover iSCSI targets:**
```shell
iscsiadm -m discovery -t st -p 10.10.10.10
# Output: 10.10.10.10:3260,1 iqn.2000-01.com.synology:NAS.default-target.1
```

**Log in to a discovered target:**
```shell
iscsiadm -m node -T iqn.2000-01.com.synology:NAS.target.1 -p 10.10.10.10 -l
```

**View active sessions:**
```shell
iscsiadm -m session
```

**Log out of a target:**
```shell
iscsiadm -m node -T iqn.2000-01.com.synology:NAS.target.1 -p 10.10.10.10 -u
# Or logout of all sessions:
iscsiadm -m session -u
```

**Identify disks:**
```shell
lsblk -S /dev/sd*   # View disk transport types
```
