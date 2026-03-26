wait
===

Wait for a process to complete before returning.

## Description

The **wait command** is used to wait for a command to finish before returning to the terminal. This command is commonly used in shell scripting to ensure a specified command has completed before proceeding with subsequent tasks. When waiting for a job, a percent sign "%" must precede the job identifier.

### Syntax

```shell
wait (parameter)
```

### Parameters

Process or job identifier: Specifies the process ID or job number.

### Examples

Use the `wait` command to wait for job number 1 to complete before returning:

Run a sleep process in the background:

```shell
sleep 10s &
[1] 27156
```

Specify the job number:

```shell
wait %1       # Wait for job number 1 to complete
[1]+  Done                    sleep 10s
```

Specify the process ID:

```shell
wait 27156
[1]+  Done                    sleep 10s
```

Output commands for currently existing job numbers:

[jobs](./jobs.md)
