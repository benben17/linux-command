nice
===

Run a program with a modified scheduling priority

## Description

The **nice command** is used to start a process with a specific scheduling priority.

### Syntax

```shell
nice [option] [command [arguments]...]
```

### Options

```shell
-n, --adjustment=N: Add integer N to the niceness (default 10). Nice values range from -20 (highest priority) to 19 (lowest priority).
```

### Parameters

Command and Arguments: The command to be executed along with any arguments.

### Examples

Start a process with a specific priority. For example, compressing a directory while ensuring it doesn't consume too much CPU:

```shell
nice -n 19 tar zcf pack.tar.gz documents
```

The usage is simple: just prefix the original command with `nice -n <value>`. Note that for many systems, positive values indicate lower priority. To give a process the highest possible priority (requires root privileges), use `--20`:

```shell
nice -n -20 tar zcf pack.tar.gz documents
```
