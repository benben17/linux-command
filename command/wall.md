wall
===

Write a message to all users' terminals

## Description

The **wall command** is used to send a message to all users currently logged into the system. It displays the message on every terminal that is set to receive public messages. If no message is provided as an argument, the `wall` command reads from standard input until an EOF character is received.

### Syntax

```shell
wall [message]
```

### Parameters

message: The broadcast message to be sent.

### Examples

```shell
[root@localhost ~]# wall this is a test line

Broadcast message from root (pts/1) (Fri Dec 20 11:36:51 2013):

this is a test line
```
