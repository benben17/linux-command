lp
===

Print files or modify queued print jobs

## Description

The **lp** command is used to print files or modify queued print jobs. Similar to the `lpr` command, `lp` supports both file input and standard input. It differs from `lpr` in having a slightly more complex set of parameter options.

### Syntax

```shell
lp (options) (parameters)
```

### Options

```shell
-E: Force encryption when connecting to the server;
-U <username>: Specify the username to use when connecting to the print server;
-d <printer>: Specify the destination printer;
-i <job-id>: Specify an existing job ID;
-m: Send an email when the job is completed;
-n <copies>: Specify the number of copies to print;
-t <title>: Specify the name/title of the print job;
-H <when>: Specify when the job should be printed;
-P <page-list>: Specify which pages to print.
```

### Parameters

File: The file to be printed.

### Examples

To print the file `/etc/motd` on the printer `lp0` connected to device `dlp0`, enter:

```shell
lp /etc/motd
```

To print 30 copies of the `/etc/motd` file using a copy of the file and notify the user by email when the job is done, enter:

```shell
lp -c -m -n30 -d lp0:lpd0 /etc/motd
```

To print `/etc/motd` with backend flags `-f` and `-a` and the job title "blah", enter:

```shell
lp -t "blah" -o -f -o -a /etc/motd
```

To queue the file `myfile` and return the job number:

```shell
lp myfile
```

To queue the file `myfile` and suppress the job number:

```shell
lp -s myfile
```

**Exit Status**

This command returns the following exit values:
*   0: All input files were successfully processed.
*   >0: No output device was available, or an error occurred.
