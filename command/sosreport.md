sosreport
===

Collect system configuration and diagnostic information.

## Description

The **sosreport command** is a configuration and data collection utility used to gather system configuration, log files, and diagnostic information for troubleshooting and analysis. it packages the information into a compressed tar file for easy transfer and analysis. `sosreport` is the standard tool for technical support in Red Hat Enterprise Linux systems.

### Syntax

```shell
sosreport [option]
```

### Options

```shell
-l, --list-plugins     # List all available plugins
-n, --skip-plugins     # Skip specified plugins (comma-separated)
-e, --enable-plugins   # Enable specified plugins (comma-separated)
-o, --only-plugins     # Run only specified plugins (comma-separated)
-a, --alloptions       # Enable all plugin options
-v, --verbose          # Verbose output mode
-q, --quiet            # Quiet mode, reduces output
--batch                # Batch mode, do not prompt for user input
--build                # Collect system build information
--case-id=CASE_ID      # Specify a case ID
--config-file=CONFIG   # Specify configuration file path
--debug                # Debug mode
--experimental         # Enable experimental plugins
--log-size=SIZE        # Limit log file size (MB)
--plugin-timeout=TIMEOUT # Plugin timeout (seconds)
--since=DATE           # Collect logs since the specified date
--tmp-dir=DIR          # Specify temporary directory
--verify               # Verify archive integrity
-z, --compression-type # Specify compression type (gzip, bzip2, xz)
```

### Common Options

```shell
-a     # Enable all plugin options for most comprehensive collection
-v     # Verbose mode, show the collection process
-q     # Quiet mode, minimize output
--batch # Batch mode, no user interaction required
```

### Examples

Collect system diagnostic information:

```shell
sosreport
```

Collect information in batch mode (no user interaction):

```shell
sosreport --batch
```

Collect information in verbose mode:

```shell
sosreport -v
```

Enable all plugin options to collect complete information:

```shell
sosreport -a
```

Collect only network-related information:

```shell
sosreport -o network
```

Skip certain plugins:

```shell
sosreport -n rpm,yum
```

Collect logs since a specific date:

```shell
sosreport --since="2023-01-01"
```

Specify case ID and use batch mode:

```shell
sosreport --batch --case-id=12345678
```

List all available plugins:

```shell
sosreport -l
```

Collect system information and limit log file size:

```shell
sosreport --log-size=100
```

Use a different compression type:

```shell
sosreport -z xz
```

### Common Plugins

```shell
block          # Block device information
boot           # Boot-related information
kernel         # Kernel information
logs           # System logs
memory         # Memory information
network        # Network configuration
networking     # Network diagnostics
process        # Process information
processor      # CPU information
rpm            # RPM package information
system         # System configuration
yum            # YUM package manager information
```

### Output File

`sosreport` generates a compressed tar file in the `/var/tmp/` directory with a filename format like:
```
sosreport-<hostname>-<timestamp>-<hash>.tar.xz
```

### Precautions

- `sosreport` requires root privileges to run.
- The collected information may contain sensitive data; ensure security before transmission.
- Generated files can be large; ensure sufficient disk space.
- By default, sensitive information (such as passwords, keys) is obfuscated.
