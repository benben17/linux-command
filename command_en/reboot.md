# reboot

Restart the running Linux operating system.

## Description

The **reboot** command is used to restart the currently running Linux operating system.

### Syntax

```shell
reboot [options]
```

### Options

```shell
-d: Reboot without writing data to the record file /var/log/wtmp. This implies the '-n' option.
-f: Force reboot without calling the shutdown command.
-i: Shut down all network interfaces before rebooting.
-n: Do not check for unclosed processes before rebooting.
-w: Test only; do not actually reboot the system. Only write the reboot record to the /var/log/wtmp file.
```

### Examples

```shell
reboot        # Reboot the system
reboot -w     # Simulate a reboot (writes a record only, does not actually reboot)
```
