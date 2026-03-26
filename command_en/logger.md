logger
===

Enter messages into the system log

## Description

The **logger** command is used to write messages to the system log. It provides a shell command interface to the `syslog` system module.

### Syntax

```shell
logger [options] [message]
```

### Options

```shell
 -T, --tcp             Use TCP
 -d, --udp             Use UDP
 -i, --id              Log the process ID of the logger process on each line
 -f, --file <file>     Log the contents of the specified file
 -h, --help            Display help and exit
 -n, --server <name>   Write to the specified remote syslog server using UDP
 -P, --port <port>     Use the specified UDP port (default is 514)
 -p, --priority <prio> Specify the priority of the message (e.g., "facility.level").
                       Example: "-p local3.info". Default is "user.notice"
 -s, --stderr          Output message to standard error as well as the system log
 -t, --tag <tag>       Mark every line to be logged with the specified tag
 -u, --socket <socket> Write to the specified socket instead of the system log routine
 -V, --version         Display version information and exit
```

### Examples

```shell
logger -p syslog.info "backup.sh is starting"
```
