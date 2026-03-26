logwatch
===

A customizable and pluggable log monitoring system

## Description

The **logwatch** command is a customizable and pluggable log monitoring system that generates reports by analyzing system log files over a given time range. By default, `logwatch` runs once a day via `/etc/cron.daily`.

### Syntax

```shell
logwatch (options)
```

### Options

```shell
--detail <level>: Specify the level of detail for the report (e.g., Low, Medium, High);
--logfile <file>: Process only the specified log file;
--service <name>: Process only logs for the specified service;
--print: Print the report to standard output;
--mailto <address>: Send the report to the specified email address;
--range <range>: Specify the date range for logs (e.g., Yesterday, Today, All);
--archives: Process archived log files as well;
--debug <level>: Enable debug mode with a specific level;
--save <filename>: Save the report to a file instead of displaying or emailing it;
--logdir <dir>: Specify the directory to search for logs (overrides default);
--hostname <name>: Use the specified hostname in the report;
--numeric: Display IP addresses instead of hostnames in the report;
--help: Display help information.
```

### Examples

Check if Logwatch is installed (Red Hat usually has it pre-installed, though it might be an older version):

```shell
rpm -qa logwatch
```

If it's not installed:

```shell
rpm -ivh logwatch***.rpm
```

To update an existing version:

```shell
rpm -Uvh logwatch***.rpm
```

**Configuration:**

You can customize Logwatch by adding configurations to `/etc/logwatch/conf/logwatch.conf` (which overrides `/usr/share/logwatch/default.conf/logwatch.conf`). You can also specify settings directly on the command line.

```shell
# Display a high-detail report for all services and ranges
logwatch --detail High --Service All --range All --print

# View logs specifically for the sshd service with high detail
logwatch --service sshd --detail High
```
