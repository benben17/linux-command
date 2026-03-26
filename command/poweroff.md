poweroff
===

Power off the Linux system. The shutdown record is written to the /var/log/wtmp log file.

## Description

The **poweroff command** is used to shut down the Linux system.

### Syntax

```shell
poweroff [options]
```

### Options

```shell
-n Do not sync before power-off
-p Power off the system (when called as halt)
-v Increase output, including messages
-q Decrease output, only error messages
-w Do not actually power off the system, only write to /var/log/wtmp
-f Force power-off, does not call shutdown
```

### Example

Power off the Linux system.

```shell
[root@localhost ~]# poweroff
```
