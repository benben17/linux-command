suspend
===

Suspend execution of the shell

## Summary

```shell
suspend [-f]
```

## Description

- Suspends the execution of the shell until a `SIGCONT` signal is received.
- Cannot be used on a `login shell` unless the `-f` option is used.

## Options

```shell
-f: Force suspension of a login shell.
```

## Return Value

Returns success unless job control is not enabled or an error occurs.

## Examples

```shell
# Open a terminal and get the PID
echo $$
# Suspend execution
suspend
```

```shell
# Open another terminal and send SIGCONT signal
kill -s SIGCONT <PID>
# The original terminal will resume and allow interaction.
```

### Notes

1. Bash job control commands include `bg`, `fg`, `kill`, `wait`, `disown`, and `suspend`.
2. This command requires the `monitor` option to be enabled. Check status with `set -o` and looking at the `monitor` row; enable with `set -o monitor` or `set -m`.
3. This is a bash builtin. Use the `help` command for related information.
