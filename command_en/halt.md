halt
===

Shut down the running Linux operating system.

## Supplemental Information

The **halt command** is used to shut down the running Linux operating system. It first checks the system's current runlevel; if the runlevel is 0 or 6, it shuts down the system directly. Otherwise, it calls `shutdown` to perform the shutdown process.

### Syntax

```shell
halt (options)
```

### Options

```shell
-d: Do not record the action in wtmp;
-f: Force shutdown without calling shutdown, regardless of the current runlevel;
-i: Shut down all network interfaces before halting;
-n: Do not perform a sync before halting;
-p: Execute poweroff after halting;
-w: Only record the action in wtmp without actually halting the system.
```

### Examples

```shell
halt -p     # Shut down the system and turn off the power.
halt -d     # Shut down the system without leaving a record in wtmp.
```
