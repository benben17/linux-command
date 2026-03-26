lpr
===

Submit files for printing

## Description

The **lpr** command is used to send files to a specified printer for printing. If no destination printer is specified, the default printer is used.

### Syntax

```shell
lpr (options) (parameters)
```

### Options

```shell
-E: Force encryption when connecting to the print server;
-H <server>: Specify an optional print server;
-C <title>: Specify the name of the print job;
-P <printer>: Specify the destination printer for the job;
-U <username>: Specify an optional username;
-# <copies>: Specify the number of copies to print;
-h: Disable banner printing;
-m: Send an email after the job is completed;
-r: Remove the file after printing is finished.
```

### Parameters

File: The file to be printed.

### Examples

Print `man1` and `man2` on the printer `lp`:

```shell
lpr -P lp man1 man2
```
