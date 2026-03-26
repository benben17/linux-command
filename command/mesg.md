mesg
===

Control write access to your terminal

## Description

The **mesg command** is used to control whether other users are allowed to send messages to your terminal using the `write` or `talk` commands. Setting `mesg` to `y` allows messages to be displayed directly on your screen, while `n` prohibits them.

### Syntax

```shell
mesg [y|n]
```

### Parameters

y/n: `y` allows write access to the terminal; `n` prohibits it.

### Examples

```shell
[root@localhost ~]# mesg y    # Allow other users to send messages to your terminal.
[root@localhost ~]# mesg n    # Prohibit other users from sending messages to your terminal.
```
