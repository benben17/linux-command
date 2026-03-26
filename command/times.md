times
===

Display process accumulated time.

## Main Purpose

- Print the accumulated user and system time used by the shell and its child processes.

## Return Value

Always returns success.

## Example

```shell
# Execute the command
times
# Result
0m0.037s 0m0.009s
0m0.010s 0m0.024s
# According to the times(2) man page, the mapping is as follows:
# User time        | System time
# Child process user time | Child process system time
```

### Notes

1. This command is a bash built-in; see the `help` command for related help information.
