pidof
===

Finds the process ID (PID) of a running program by name.

## Description

The **pidof command** is used to find the process ID (PID) of a running program. It is particularly useful in scripts for managing processes by their names rather than manually looking up PIDs.

### Syntax

```shell
pidof [options] [program_name]
```

### Options

```shell
-s: Return only a single PID.
-c: Only return PIDs with the same root directory.
-x: Also return PIDs of shells running the named scripts.
-o: Omit the specified process ID.
```

### Parameters

Program Name: Specifies the name of the process to search for.

### Examples

```shell
pidof nginx
13312 5371

pidof crond
1509

pidof init
1
```
