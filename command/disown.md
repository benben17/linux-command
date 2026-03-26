disown
===

Remove jobs from the current shell.

## Synopsis

```shell
disown [-h] [-ar] [jobspec ... | pid ...]
```

## Description

- Remove all jobs from the current shell's job list.
- Remove one or more specified jobs from the current shell's job list.
- Remove running jobs from the current shell's job list.
- Mark jobs so that they will not be terminated when the shell exits.

## Options

```shell
-h    Mark each job so that SIGHUP is not sent to the job if the shell receives a SIGHUP.
-a    Remove all jobs.
-r    Remove only running jobs.
```

## Parameters

jobspec (Optional): One or more job identifiers to remove.
pid (Optional): One or more process IDs corresponding to the jobs to remove.

## Return Value

Returns success unless job control is not enabled or an error occurs.

## Examples

```shell
# Demonstration.
[user2@pc] ssh 192.168.1.4
user2@192.168.1.4's password:
# Press Ctrl+Z to stop the interactive session.
[1]+  Stopped                 ssh 192.168.1.4

[user2@pc] ssh 192.168.1.7
user2@192.168.1.7's password:
# Press Ctrl+Z to stop the interactive session.
[2]+  Stopped                 ssh 192.168.1.7

[user2@pc] sleep 120 &
[3] 28986

# List jobs and PID information.
[user2@pc] jobs -l
[1]- 28756 Stopped                 ssh 192.168.1.4
[2]+ 28833 Stopped                 ssh 192.168.1.7
[3]  28986 Running                 sleep 120 &

# Remove running jobs.
[user2@pc] disown -r

[user2@pc] jobs -l
[1]- 28756 Stopped                 ssh 192.168.1.4
[2]+ 28833 Stopped                 ssh 192.168.1.7

# Note that disown only removes the job from the job list; it does not stop the process.
[user2@pc] pgrep -a -u user2 -f 'sleep 120'
28986 sleep 120

# Remove a specific job.
[user2@pc] disown %2
bash: warning: deleting stopped job 2 with process group 28833

[user2@pc] jobs -l
[1]- 28756 Stopped                 ssh 192.168.1.4

# Note that disown only removes the job; it does not stop the process.
[user2@pc] pgrep -a -u user2 -f 'ssh 192.168.1.7'
28833 ssh 192.168.1.7

# Remove all jobs.
[user2@pc] disown -a
bash: warning: deleting stopped job 1 with process group 28756

[user2@pc] jobs -l

# Note that disown only removes the jobs; it does not stop the processes.
[user2@pc] pgrep -a -u user2 -f 'ssh 192.168.1.4'
28756 ssh 192.168.1.4
```

```shell
# Demonstration of the -h option.
[user2@pc] sleep 90 &
[1] 109080

[user2@pc] jobs -l
[1]+ 109080 Running                 sleep 90 &

[user2@pc] disown -h %1

[user2@pc] exit

# The previous terminal is closed. Open a new terminal to search for the job.
[user2@pc] pgrep -a -u user2 -f 'sleep 90'
109080 sleep 90
```

### Notes

1. Bash job control commands include `bg`, `fg`, `kill`, `wait`, `disown`, and `suspend`.
2. This command requires the `monitor` option to be enabled. Check the status with `set -o`. Enable it with `set -o monitor` or `set -m`.
3. This is a Bash built-in command. For more help, use the `help` command.

### References

- [disown command examples](https://www.cyberciti.biz/faq/unix-linux-disown-command-examples-usage-syntax/)
