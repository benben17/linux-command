atrm
===

Delete specified tasks from the pending task queue

## Additional Information

The **atrm command** is used to delete specified tasks from the pending task queue.

### Syntax

```shell
atrm (options) (parameters)
```

### Options

```shell
-V: Display version number.
```

### Parameters

Job number: Specifies the task to be deleted from the pending queue.

### Examples

Delete already queued tasks:

```shell
atq        # Display currently set tasks
2 Mon May 17 08:00:00 2010 a root
1 Sat May 15 17:00:00 2010 a root

atrm 2     # Delete task 2
```
