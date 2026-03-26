pkill
===

Signals processes based on name and other attributes.

## Description

The **pkill command** allows you to kill or send signals to processes by their name. It works similarly to `killall`, targeting all running instances of a program. If you need to kill a specific single process, use its PID with the `kill` command.

### Syntax

```shell
pkill [options] [pattern]
```

### Options

```shell
-o: Signal only the oldest (least recently started) of the matching processes.
-n: Signal only the newest (most recently started) of the matching processes.
-P: Signal only processes whose parent process ID matches the given list.
-g: Signal only processes in the specified process groups.
-t: Signal only processes running on the specified terminal.
```

### Parameters

Process Name: The pattern to match against the process names (supports regular expressions).

### Examples

**Find a process PID by name:**
```shell
pgrep -l gaim
2979 gaim
```

**Kill the process by name:**
```shell
pkill gaim
```

In summary: `kill` targets a PID, while `pkill` targets a command name or pattern.
