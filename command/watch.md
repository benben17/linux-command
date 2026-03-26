watch
===

Execute a program periodically, showing output fullscreen

## Description

The **watch command** runs a specified command repeatedly, displaying its output in full-screen mode. It is a very useful tool included in almost all Linux distributions. As its name suggests, `watch` allows you to monitor the output of a command without having to run it manually over and over again.

### Syntax

```shell
watch [options] [command]
```

### Options

```shell
-n, --interval <seconds>  Specify the update interval. The default is 2 seconds.
-d, --differences [=cumulative]  Highlight changes between updates. The 'cumulative' option highlights all changes since the start.
-t, --no-title  Turn off the header showing the interval, command, and current time.
-h, --help  Display help documentation.
```

### Parameters

command: The command to be executed periodically.

### Examples

```shell
watch -n 1 -d netstat -ant      # Update every second and highlight changes in network connections
watch -n 1 -d 'pstree|grep http' # Update every second and highlight changes in http connections. Use quotes if the command contains pipes.
watch 'netstat -an | grep :21 | grep <IP> | wc -l' # Real-time view of connections from a specific IP
watch -d 'ls -l|grep scf'       # Monitor changes to files containing 'scf' in the current directory
watch -n 10 'cat /proc/loadavg' # Output system load average every 10 seconds
watch uptime
watch -t uptime
watch -d -n 1 netstat -ntlp
watch -d 'ls -l | fgrep goface'     # Monitor 'goface' files
watch -t -differences=cumulative uptime
watch -n 60 from            # Monitor mail
watch -n 1 "df -i;df"       # Monitor disk inode and block usage changes
```

Note: On FreeBSD, the `watch` command is used to observe what another user is doing on their terminal, which requires root privileges. In Linux, it is used to execute programs periodically.
