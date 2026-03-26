renice
===

Modifies the scheduling priority of running processes.

## Description

The **renice command** can modify the scheduling priority of running processes. By default, processes are specified by their process ID (PID). You can also specify process groups or usernames to adjust the priority level for all processes belonging to that group or user. Only the system administrator can change the priority of other users' processes, and only the system administrator can set negative priority levels.

### Syntax

```shell
renice(options)(parameters)
```

### Options

```shell
-g: Specifies the process group ID;
-p <PID>: Changes the priority level of the specified process; this is the default.
-u: Specifies the username of the user who started the processes.
```

### Parameters

Process ID: Specifies the process whose priority is to be modified.

### Examples

Add 1 to the priority of processes with IDs 987 and 32, and processes owned by users `daemon` and `root`:

```shell
renice 1 987 -u daemon root -p 32
```

Note: Every process has a unique ID.
