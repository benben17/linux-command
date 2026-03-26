bg
===

Move foreground jobs to the background.

## Synopsis

```shell
bg [job_spec ...]
```

## Main Purpose

- Used to place jobs in the background, allowing other tasks to be executed in the foreground. The effect of running this command is the same as adding the symbol `&` after a command, both of which execute it in the system background.

- If there is only one job in the background, the job ID can be omitted when using this command.

## Parameters

job_spec (optional): Specifies the identifier of the job(s) to be moved to the background for execution. Multiple identifiers can be specified.

## Return Value

Returns success unless job control is not enabled or an error occurs.

## Examples

```shell
# Run the sleep command, then press Ctrl+z.
sleep 60
^Z
[1]+  Stopped                 sleep 60

# Use the bg command to make the job run in the background.
bg %1

# Return information:
[1]+ sleep 60 &
```

### Notes

1. Bash's job control commands include `bg`, `fg`, `kill`, `wait`, `disown`, and `suspend`.
2. This command requires the `monitor` option of `set` to be enabled; check the job control status by typing `set -o` and looking for the `monitor` line; execute `set -o monitor` or `set -m` to enable this option.
3. This command is a bash built-in; for related help information, please use the `help` command.
