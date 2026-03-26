ipcrm
===

Remove message queues, semaphore sets, or shared memory segments.

## Description

The `ipcrm` command is used to remove one or more System V interprocess communication (IPC) objects from the system.

### Syntax

```shell
ipcrm [ -m SharedMemoryID ] [ -M SharedMemoryKey ] [ -q MessageID ] [ -Q MessageKey ] [ -s SemaphoreID ] [ -S SemaphoreKey ]
```

### Options

```shell
-m id : Remove the shared memory segment associated with ID.
-M key : Remove the shared memory segment associated with key.
-q id : Remove the message queue associated with ID.
-Q key : Remove the message queue associated with key.
-s id : Remove the semaphore set associated with ID.
-S key : Remove the semaphore set associated with key.
```

IDs and keys can be found using the `ipcs` command.

### Examples

To remove the shared memory segment with ID 18602:

```shell
ipcrm -m 18602
```
