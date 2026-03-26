mailq
===

Display the mail queue

## Description

The **mailq command** displays a list of messages that are waiting to be sent. Each entry includes the queue ID, size, arrival time, sender, and recipients. If a message failed to be delivered during the last attempt, the reason for the failure is also shown.

### Syntax

```shell
mailq [OPTION]
```

### Options

```shell
-v: Display detailed information.
```

### Examples

```shell
[root@localhost ~]# mailq -v
/var/spool/mqueue is empty
                Total requests: 0
```
