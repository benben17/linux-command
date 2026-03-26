fg
===

Move background jobs to the foreground for execution.

## Synopsis

```shell
fg [job_spec ...]
```

## Main Purpose

- Move background jobs (either running in the background or suspended) to the foreground terminal for execution.

- If there is only one background task, the task ID can be omitted.

## Parameters

job_spec (Optional): Specifies the job identifier(s) to be moved to the foreground. One or more can be specified.

## Return Value

Returns the execution status of the job; returns failure if an error occurs.

## Examples

```shell
# Run the sleep command, then press ctrl+z.
sleep 60
^Z
[1]+  Stopped                 sleep 60

# Use the fg command to move the job to the foreground.
fg %1

# Output:
sleep 60
```

### Note

1. `bash` job control commands include `bg`, `fg`, `kill`, `wait`, `disown`, and `suspend`.
2. This command requires the `set` option `monitor` to be enabled; check the job control status by typing `set -o` and looking for the `monitor` line; execute `set -o monitor` or `set -m` to enable this option.
3. This command is a bash built-in; for related help information, please refer to the `help` command.
