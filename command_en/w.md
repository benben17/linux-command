w
===

Display information about the users currently logged into the system.

## Description

The **w command** is used to display a list of users currently logged into the system and the commands they are executing. Running this command provides information on who is logged in and what programs they are running. Running `w` alone shows all users; you can also specify a username to show information for that user only.

### Syntax

```shell
w (option) (parameter)
```

### Options

```shell
-h, --no-header     Do not print the header;
-u, --no-current    Ignore the username when displaying current process and CPU time;
-s, --short         Use the short output format;
-f, --from          Show where the user logged in from;
-o, --old-style     Old-style output;
-i, --ip-addr       Display IP addresses instead of hostnames (if possible);

    --help          Display this help and exit;
-V, --version       Display version information.
```

### Parameters

User: Only display information for the specified user.

### Examples

```shell
w
 20:39:37 up 136 days,  3:58,  1 user,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM              login@   IDLE   JCPU   PCPU WHAT
root     pts/0    222.94.97.122    20:39    1.00s  0.00s  0.00s w
```
