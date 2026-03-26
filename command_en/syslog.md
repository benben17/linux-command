syslog
===

The default system log daemon

## Description

**syslog** is the default logging facility for Linux systems. The default configuration file is `/etc/syslog.conf`. Programs, daemons, and the kernel provide access to system log information. Therefore, any program that wants to generate log information can call the syslog interface.

Almost all network devices can send log information to a remote server via the syslog protocol using User Datagram Protocol (UDP). The remote log server must listen on UDP port 514 and process the logs according to its `syslog.conf` configuration. This allows events to be logged to one or more servers for offline analysis.

Typically, syslog receives information from various system functions, each including a priority level. The `/etc/syslog.conf` file instructs `syslogd` how to report information based on the facility and priority level.

### Usage

Creating and writing logs in `/var/log` is handled by the syslog protocol and executed by the `syslogd` daemon. Every standard process can use syslog for logging. The `logger` command can be used to record logs via `syslogd`.

To log a message to `/var/log/messages`:

```shell
logger this is a test log line

Output:
tail -n 1 messages
Jan  5 10:07:03 localhost root: this is a test log line
```

To log with a specific tag:

```shell
logger -t TAG this is a test log line

Output:
tail -n 1 messages
Jan  5 10:37:14 localhost TAG: this is a test log line
```
