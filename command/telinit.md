telinit
===

Change the system runlevel

## Description

The **telinit command** is used to change the current runlevel of a running Linux system.

The `RUNLEVEL` parameter should be one of the multi-user runlevels `2-5`, `0` to halt the system, `6` to reboot, or `1` for single-user mode.

Typically, you should use the `shutdown(8)` utility to halt, reboot, or enter single-user mode.

`RUNLEVEL` can also be `S` or `s`, which puts the system directly into single-user mode without stopping processes first, which is generally not recommended.

Runlevels are changed by issuing a `runlevel(7)` event, which includes the new runlevel in the `RUNLEVEL` environment variable and the previous runlevel in `PREVLEVEL` (obtained from the environment or `/var/run/utmp`).

`telinit` writes the new runlevel to `/var/run/utmp` and appends a new entry to `/var/log/wtmp`.

### Syntax

```shell
telinit [OPTION]... RUNLEVEL
```

### Options

```shell
-t: Specify the number of seconds to wait.
-e KEY=VALUE: Specify additional environment variables to include in the event along with RUNLEVEL and PREVLEVEL.
```

### Parameters

Runlevel: Specify the runlevel to switch to.

### Environment

RUNLEVEL

If set, `telinit` reads the current runlevel from this environment variable rather than `/var/run/utmp`.

### Files

- `/var/run/utmp`: Where the current runlevel is read from; this file is also updated with the new runlevel.
- `/var/log/wtmp`: Records of the new runlevel are appended to this file.
吐
