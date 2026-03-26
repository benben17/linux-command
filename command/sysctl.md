sysctl
===

Configure kernel parameters at runtime

## Description

The **sysctl command** is used to modify kernel parameters at runtime. Available kernel parameters are listed under the `/proc/sys/` directory. It includes advanced options for the TCP/IP stack and virtual memory system, allowing experienced administrators to significantly improve system performance. More than five hundred system variables can be read and set using `sysctl`.

### Syntax

```shell
sysctl (options) (parameters)
```

### Options

```shell
-n: Print only the value, not the key.
-e: Ignore errors about unknown keys.
-N: Print only the name.
-w: Use this when changing sysctl settings.
-p: Load kernel parameter settings from the configuration file "/etc/sysctl.conf".
-a: Print all currently available kernel parameters and their values.
-A: Print all currently available kernel parameters in a table format.
```

### Parameters

variable=value: Set the value for a specific kernel parameter.

### Examples

List all readable variables:

`sysctl -a`

Read a specific variable, such as `kern.maxproc`:

`sysctl kern.maxproc`
`kern.maxproc: 1044`

To set a variable, use the `variable=value` syntax:

```shell
sysctl kern.maxfiles=5000
kern.maxfiles: 2088 -> 5000
```

You can use `sysctl` to modify system variables directly or edit the `sysctl.conf` file. `sysctl.conf` uses the `variable=value` format. Values specified in this file are set after the system enters multi-user mode. Note that not all variables can be set in this mode.

`sysctl` variables are typically strings, numbers, or booleans (1 for 'yes', 0 for 'no').

```shell
sysctl -w kernel.sysrq=0
sysctl -w kernel.core_uses_pid=1
sysctl -w net.ipv4.conf.default.accept_redirects=0
sysctl -w net.ipv4.conf.default.accept_source_route=0
sysctl -w net.ipv4.conf.default.rp_filter=1
sysctl -w net.ipv4.tcp_syncookies=1
sysctl -w net.ipv4.tcp_max_syn_backlog=2048
sysctl -w net.ipv4.tcp_fin_timeout=30
sysctl -w net.ipv4.tcp_synack_retries=2
sysctl -w net.ipv4.tcp_keepalive_time=3600
sysctl -w net.ipv4.tcp_window_scaling=1
sysctl -w net.ipv4.tcp_sack=1
```

### Configuring sysctl

Edit the file: `/etc/sysctl.conf`

Example configuration:

```shell
# Controls source route verification
net.ipv4.conf.default.rp_filter = 1

# Disables IP source routing
net.ipv4.conf.default.accept_source_route = 0

# Controls the System Request debugging functionality of the kernel
kernel.sysrq = 0

# Controls whether core dumps will append the PID to the core filename.
kernel.core_uses_pid = 1

# Disable ICMP Redirect Acceptance
net.ipv4.conf.default.accept_redirects = 0

# Enable Log Spoofed Packets, Source Routed Packets, Redirect Packets
net.ipv4.conf.default.log_martians = 1

# Decrease the time default value for tcp_fin_timeout connection
net.ipv4.tcp_fin_timeout = 25

# Decrease the time default value for tcp_keepalive_time connection
net.ipv4.tcp_keepalive_time = 1200

# Turn on the tcp_window_scaling
net.ipv4.tcp_window_scaling = 1

# Turn on the tcp_sack
net.ipv4.tcp_sack = 1

# tcp_fack should be on because of sack
net.ipv4.tcp_fack = 1

# Turn on the tcp_timestamps
net.ipv4.tcp_timestamps = 1

# Enable TCP SYN Cookie Protection
net.ipv4.tcp_syncookies = 1

# Enable ignoring broadcasts request
net.ipv4.icmp_echo_ignore_broadcasts = 1

# Enable bad error message Protection
net.ipv4.icmp_ignore_bogus_error_responses = 1

# Set TCP Re-Ordering value in kernel to ‘5′
net.ipv4.tcp_reordering = 5

# Lower syn retry rates
net.ipv4.tcp_synack_retries = 2
net.ipv4.tcp_syn_retries = 3

# Set Max SYN Backlog to ‘2048′
net.ipv4.tcp_max_syn_backlog = 2048

# Various Settings
net.core.netdev_max_backlog = 1024

# Increase the maximum number of skb-heads to be cached
net.core.hot_list_length = 256

# Increase the tcp-time-wait buckets pool size
net.ipv4.tcp_max_tw_buckets = 360000

# Socket buffer memory allocation
net.core.rmem_default = 65535
net.core.rmem_max = 8388608
net.ipv4.tcp_rmem = 4096 87380 8388608
net.core.wmem_default = 65535
net.core.wmem_max = 8388608
net.ipv4.tcp_wmem = 4096 65535 8388608
net.ipv4.tcp_mem = 8388608 8388608 8388608
net.core.optmem_max = 40960
```

To ignore ping requests:

```shell
# Disable ping requests
net.ipv4.icmp_echo_ignore_all = 1
```

Apply changes immediately:

```shell
/sbin/sysctl -p
/sbin/sysctl -w net.ipv4.route.flush=1
```
