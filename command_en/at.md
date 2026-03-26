at
===

Execute a task at a specified time

## Additional Information

The **at command** is used to execute commands at a specified time. `at` allows for a fairly complex set of time specification methods. It can accept time in the `hh:mm` (hour:minute) format for the current day. If that time has already passed, it will be executed the next day. You can also use vague terms like `midnight`, `noon`, or `teatime` (usually 4 PM) to specify the time. Users can also use 12-hour format, adding `AM` or `PM` after the time. Specific dates for command execution can also be specified in formats like `month day`, `mm/dd/yy`, or `dd.mm.yy`. The specified date must follow the specified time.

The above are all absolute timing methods; relative timing can also be used, which is useful for scheduling commands to be executed soon. The format is: `now + count time-units`, where `now` is the current time and `time-units` are units of time such as `minutes`, `hours`, `days`, or `weeks`. `count` is the quantity of time. Another timing method is directly using `today` or `tomorrow` to specify the completion time for the command.

### Syntax

```shell
at [-V] [-q queue] [-f file] [-mldbv] time at -c job [job...]
```

### Options

```shell
-f: Specify a task file containing specific instructions.
-q: Specify the queue name for the new task.
-l: Display a list of pending tasks.
-d: Delete the specified pending task.
-m: Send an email to the user after the task is completed.
```

### Parameters

Date/Time: Specifies the date and time for task execution.

### Examples

Execute `/bin/ls` at 5 PM three days from now:

```shell
[root@localhost ~]# at 5pm+3 days
at> /bin/ls
at> <EOT>
job 7 at 2013-01-08 17:00
```

Tomorrow at 5:20 PM, output the date to a specified file:

```shell
[root@localhost ~]# at 17:20 tomorrow
at> date >/root/2013.log
at> <EOT>
job 8 at 2013-01-06 17:20
```

After scheduled tasks are set, you can use the `atq` command to view tasks that have not yet been executed:

```shell
[root@localhost ~]# atq
8       2013-01-06 17:20 a root
7       2013-01-08 17:00 a root
```

Delete a set task:

```shell
[root@localhost ~]# atrm 7
[root@localhost ~]# atq
8       2013-01-06 17:20 a root
```

Display the content of a set task:

```shell
[root@localhost ~]# at -c 8
#!/bin/sh
# atrun uid=0 gid=0
# mail     root 0
umask 22
date >/root/2013.log
```

Execute a task using a task file:

```shell
[root@localhost ~]# echo "/bin/ls" > mytask.txt
[root@localhost ~]# at -f mytask.txt 5pm+3 days
job 9 at 2013-01-08 17:00
```

Execute a task specifying a task queue:

```shell
[root@localhost ~]# at -q b 5pm+3 days
at> /bin/ls
at> <EOT>
job 10 at 2013-01-08 17:00
```

Send an email notification after the task is completed:

```shell
[root@localhost ~]# at -m 5pm+3 days
at> /bin/ls
at> <EOT>
job 11 at 2013-01-08 17:00
```
