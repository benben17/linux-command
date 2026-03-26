batch
===

Execute commands when system load levels permit.

## Description

The **batch command** is used to execute tasks at a specified time when the system is not busy. Its usage is similar to `at`.

### Syntax

```shell
batch [options] [parameters]
```

### Options

```shell
-f: Specify a file containing the task commands.
-q: Specify the queue name for the new task.
-m: Send an email to the user after the task is completed.
```

### Parameters

Date and Time: Specify the date and time for the task to be executed.

### Examples

```shell
batch 
at> echo 1234
at> <EOT>
job 5 at Sun Apr 28 08:49:00 2013
```
