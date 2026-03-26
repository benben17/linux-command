atq
===

List the current user's at task list

## Additional Information

The **atq command** displays the list of pending tasks in the system, which is the list of at tasks for the current user.

### Syntax

```shell
atq [-V] [-q queue] [-v]
```

### Options

```shell
-V: Display version number.
-q: Query tasks in a specified queue.
```

### Examples

Create a task to be executed in 10 minutes and list the current user's task list:

```shell
[root@localhost ~]# at now + 10 minutes
at> echo 1111
at> <EOT>
job 3 at Fri Apr 26 12:56:00 2013
```

Use the `atq` command to view the current user's task list:

```shell
[root@localhost ~]# atq
3       Fri Apr 26 12:56:00 2013 a root
```

Query tasks in a specified queue:

```shell
[root@localhost ~]# at -q a now + 10 minutes
at> echo "Task in queue a"
at> <EOT>
job 4 at Fri Apr 26 13:06:00 2013
```

Use the `atq` command to view tasks in queue `a`:

```shell
[root@localhost ~]# atq -q a
4       Fri Apr 26 13:06:00 2013 a root
```

Display the version number of the `atq` command:

```shell
[root@localhost ~]# atq -V
atq (GNU at) 3.1.20
```
