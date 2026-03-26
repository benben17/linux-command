pgrep
===

Finds or signals processes based on name and other attributes.

## Description

The **pgrep command** looks through the currently running processes and lists the process IDs (PIDs) which match the selection criteria. Each PID is displayed as a decimal number, followed by a newline (by default).

### Syntax

```shell
pgrep [options] [pattern]
```

### Options

```shell
-d, --delimiter <string>: Specify the output delimiter.
-l, --list-name: List the process ID and the process name.
-a, --list-full: List the process ID and the full command line.
-v, --inverse: Invert the match (show processes that do not match).
-w, --lightweight: List all thread IDs (TIDs).
-c, --count: Show the number of matching processes.
-f, --full: Match against the full command line instead of just the process name.
-g, --pgroup <PGID,...>: Match specified process group IDs.
-G, --group <GID,...>: Match real group IDs.
-i, --ignore-case: Match case-insensitively.
-n, --newest: Select the most recently started process.
-o, --oldest: Select the least recently started process.
-O, --older <seconds>: Select processes older than the specified seconds.
-P, --parent <PPID,...>: Match only child processes of the specified parent PIDs.
-s, --session <SID,...>: Match session IDs.
-t, --terminal <tty,...>: Match by controlling terminal.
-u, --euid <ID,...>: Match effective user IDs.
-U, --uid <ID,...>: Match real user IDs.
-x, --exact: Match the process name exactly.
-F, --pidfile <file>: Read PIDs from a file.
```

### Parameters

Process Name: The pattern to search for (supports regular expressions).

### Examples

List PID and name of `httpd` processes:

```shell
pgrep -l httpd
```

Find the newest `httpd` process:

```shell
pgrep -ln httpd
```

Match exactly the name `httpd`:

```shell
pgrep -x httpd
```
