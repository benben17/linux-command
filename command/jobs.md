jobs
===

Display the status of jobs in the current session.

## Synopsis

```shell
jobs [-lnprs] [jobspec ...]
jobs -x command [args]
```

## Description

- Displays the status of jobs.
- Lists active jobs.
- Lists stopped jobs.

## Options

```shell
-l : Include Process IDs (PIDs) in the job information.
-n : Display only jobs that have changed status since the last notification.
-p : Display only the PIDs of the jobs.
-r : Display only running jobs.
-s : Display only stopped jobs.
```

## Return Value

Returns success unless invalid options are given or an error occurs. If using `jobs -x command [args]`, the return value is the exit status of the `command`.

## Examples

```shell
[user@pc] sleep 60 &
[1] 13338

[user@pc] jobs
[1]   Running                 sleep 60 &

[user@pc] jobs -l
[1]  13338 Running                 sleep 60 &

[user@pc] jobs -p
13338
```

### Notes

1. Bash job control commands include `bg`, `fg`, `kill`, `wait`, `disown`, and `suspend`.
2. This command requires the `monitor` option to be enabled (it is by default in interactive shells). Check with `set -o monitor`.
3. `jobs` is a shell builtin. See `help jobs` for more information.
