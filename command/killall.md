killall
===

Kill a group of processes by their name

## Description

The **killall** command kills processes by their name. It can be used to kill a group of processes with the same name. While we can use the `kill` command to kill a process with a specific PID, we often need to use commands like `ps` combined with `grep` to find the PID first. **killall** combines these two steps into one, making it a very useful command.

### Syntax

```shell
killall (options) (parameters)
```

### Options

```shell
-e: Exact match for long names;
-I: Ignore case;
-p: Kill the process group to which the process belongs;
-i: Interactive kill, requires confirmation before killing each process;
-l: Print a list of all known signals;
-q: Quiet mode, do not output anything if no processes were killed;
-r: Use regular expressions to match the names of processes to be killed;
-s: Use the specified signal instead of the default "SIGTERM";
-u: Kill processes belonging to the specified user.
```

### Parameters

Process name: Specify the name of the process to be killed.

### Examples

```shell
# Kill all processes with the same name
killall vi
# Specify the signal to send to the processes
killall -9 vi
# Signal 0 does not send a signal to the process, but can be used to check if the process exists (0 for exists, 1 for not)
killall -0 vi
echo $?
```
