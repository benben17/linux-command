rsh
===

Connect to a remote host and execute commands.

## Description

The **rsh command** is used to connect to a specified remote host and execute specified commands.

### Syntax

```shell
rsh(options)(parameters)
```

### Options

```shell
-d: Use socket-level debugging.
-l<username>: Specifies the username for logging into the remote host.
-n: Redirects input from the special device /dev/null.
```

### Parameters

*   Remote host: Specifies the remote host to connect to.
*   Command: Specifies the command to be executed on the remote host.
