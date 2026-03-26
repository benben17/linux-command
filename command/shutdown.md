shutdown
===

Command to shut down the system.

## Description

The **shutdown command** is used to shut down the system. It can close all running programs and perform a reboot or shutdown action as requested by the user.

### Syntax

```shell
shutdown [option] [parameter]
```

### Options

```shell
-c: Cancel a pending shutdown. (e.g., if "shutdown -h 11:50" was executed, use "shutdown -c" to cancel);
-f: Skip fsck on next boot;
-F: Force fsck on next boot;
-h: Shut down the system;
-k: Only send out warning messages, but do not actually shut down;
-n: Do not call init to shut down, do it by shutdown itself;
-r: Reboot after shutdown;
-t<seconds>: Delay between sending warning message and deleting information.
```

### Parameters

*   [time]: Specify when to execute the shutdown command;
*   [warning message]: Message to be sent to all logged-in users.

### Examples

Shut down immediately:

```shell
shutdown -h now
```

Shut down in 5 minutes and send a warning message to logged-in users:

```shell
shutdown +5 "System will shutdown after 5 minutes"
```
