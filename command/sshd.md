sshd
===

OpenSSH SSH daemon

## Description

The **sshd command** is the server daemon for the OpenSSH software suite.

### Syntax

```shell
sshd [option]
```

### Options

```shell
-4: Forces sshd to use IPv4 addresses only.
-6: Forces sshd to use IPv6 addresses only.
-D: Run as a background daemon.
-d: Debug mode.
-e: Send error messages to standard error instead of the system log.
-f: Specifies the server's configuration file.
-g: Specifies the grace time for clients to authenticate. If the user does not authenticate within this time, the server disconnects.
-h: Specifies a host key file.
-i: Runs sshd as an inetd service.
-o: Can be used to give options in the format used in the configuration file.
-p: Quiet mode; nothing is written to the system log.
-t: Test mode.
```
