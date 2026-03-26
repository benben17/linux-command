lprm
===

Remove jobs from the print queue

## Description

The **lprm** command is used to remove print jobs from the print queue. Jobs that have not yet been completed are kept in the queue; this command can be used to cancel those jobs.

### Syntax

```shell
lprm (options) (parameters)
```

### Options

```shell
-E: Force encryption when connecting to the print server;
-P <printer>: Specify the destination printer for the job;
-U <username>: Specify an optional username.
```

### Parameters

Job ID: Specify the print job ID to be removed.

### Examples

Remove job number 102 from printer `hpprint`:

```shell
lprm -P hpprint 102
```

Remove job number 101 from the default printer:

```shell
lprm 101
```
