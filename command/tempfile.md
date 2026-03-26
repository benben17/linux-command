tempfile
===

Naming temporary files in the shell

## Description

Sometimes when writing shell scripts, you need temporary storage for data. The most suitable location for temporary file data is `/tmp`, because all content in this directory is cleared after a system reboot. Below are two methods for generating standard filenames for temporary data.

### tempfile command

The `tempfile` command is only included by default in Debian-based distributions, such as Ubuntu. Other distributions may not have this command.

Use the `tempfile` command to name a temporary file:

```shell
temp_file_name=$(tempfile)
```

Name a temporary file with a filename that includes a random number:

```shell
temp_file_name="/tmp/file_$RANDOM"
```

`$RANDOM` is an environment variable that returns a random number.

### $$ variable

In Linux distributions without the `tempfile` command, you can use your own temporary filename:

```shell
temp_file_name="/tmp/file.$$"
```

`$$` is a pre-defined system variable that displays the process ID of the current process. Using `.$$` as a suffix will expand to the process ID of the currently running script.
