ssh-keyscan
===

Gather SSH public keys from a number of hosts

## Description

The **ssh-keyscan command** is a utility for gathering the public SSH host keys of a number of hosts.

### Syntax

```shell
ssh-keyscan [option] [host ...]
```

### Options

```shell
-4: Force ssh-keyscan to use IPv4 addresses only.
-6: Force ssh-keyscan to use IPv6 addresses only.
-f: Read addresses or hostnames from the specified file, one per line.
-p: Port to connect to on the remote host.
-T: Set the timeout for connection attempts.
-t: Specify the type of the key to fetch from the scanned hosts.
-v: Verbose mode; causes ssh-keyscan to print debugging messages.
```

### Parameters

Host List: Specifies the list of hosts from which to gather public keys.
