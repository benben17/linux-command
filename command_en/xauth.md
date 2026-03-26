xauth
===

Display and edit the authorization information used in connecting to the X server

## Description

The **xauth command** is used to display and edit the authorization information (cookies) used to connect to X servers.

### Syntax

```shell
xauth [options] [arguments]
```

### Options

```shell
-f <filename>  Specify the authority file to use instead of the default.
-q  Quiet mode. Do not print status messages.
-v  Verbose mode. Print status information during various operations.
-i  Ignore authority file locks.
-b  Break authority file locks.
```

### Subcommands (Arguments)

*   `add <display> <protocol> <hexkey>`: Add an authorization entry to the authority file.
*   `extract <filename> <display>`: Extract authorization entries for a specified display into a file.
*   `info`: Display information about the authority file.
*   `exit`: Exit the interactive mode.
*   `list [<display>]`: List authorization entries.
*   `merge <filenames>...`: Merge multiple authority files.
*   `nextract <filename> <display>`: Extract entries in numeric format.
*   `nmerge <filenames>...`: Merge entries from files in numeric format.
*   `remove <display>...`: Remove authorization entries for specified displays.
*   `source <filename>`: Read `xauth` commands from a file.
