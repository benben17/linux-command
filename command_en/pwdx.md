pwdx
===

Display the current working directory of specified processes.

## Synopsis

```shell
pwdx [PID]
```

### Parameter Description

- `PID`: The process ID to query. You can use the `ps` command to find PIDs.

## Examples

In the following example, the `ps` command is used to view information about the `nginx` process, and then the `pwdx` command is used to query the current working directory of the process with ID `5678`.

```bash
$ ps -ef | grep nginx
# root      1234     1  0 10:00 ?        00:00:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
# www-data  5678  1234  0 10:01 ?        00:00:00 nginx: worker process

$ pwdx 5678
# 5678: /var/www/html
```

View the working directory of the current process:

```bash
$ pwdx $$
```

View the working directory of a specified process:

```bash
$ pwdx 1234
```

Batch view the working directories of multiple processes:

```bash
$ ps aux | awk '{print $2}' | xargs pwdx
```

Combine with other commands to view a process's working directory and command line:

```bash
$ ps -p 1234 -o cmd | tail -n 1 | awk '{print $1}' | xargs pwdx
```

View the working directories of all processes:

```bash
$ ps -eo pid | xargs pwdx
```
