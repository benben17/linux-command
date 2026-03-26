chsh
===

Used to change the login shell

## Description

The **chsh command** is used to change the login shell for the system. If no parameters or username are specified, `chsh` will proceed in an interactive mode.

### Syntax

```shell
chsh [options] [arguments]
```

### Options

```shell
-s <shell_name> or --shell <shell_name>: Change the default shell environment for the system;
-l or --list-shells: List the shells currently available on the system;
-u or --help: Online help;
-v or --version: Display version information.
```

### Arguments

Username: The user whose default shell is to be changed.

### Examples

**Two methods to check which shells are installed on the system:**

Method 1:

```shell
[rocrocket@localhost ~]$ chsh -l
/bin/sh
/bin/bash
/sbin/nologin
/bin/zsh
```

Method 2:

```shell
[rocrocket@localhost ~]$ cat /etc/shells
/bin/sh
/bin/bash
/sbin/nologin
/bin/zsh
```

In fact, `chsh -l` simply reads this file.

**Check the shell currently in use:**

```shell
[rocrocket@localhost ~]$ echo $SHELL
/bin/bash
```

Note that `SHELL` must be in uppercase. You can see that the current shell is `/bin/bash`.

**Change my shell to zsh:**

```shell
[rocrocket@localhost ~]$ chsh -s /bin/zsh
Changing shell for rocrocket.
Password:
Shell changed.
[rocrocket@localhost ~]$
```

Use `chsh` with the `-s` option to change the login shell. You might notice that `echo $SHELL` still outputs `/bin/bash` because you need to restart your shell for the change to take full effect. `chsh -s` actually modifies the line corresponding to your username in the `/etc/passwd` file. Let's check it:

```shell
[rocrocket@localhost ~]$ cat /etc/passwd | grep ^rocrocket
rocrocket:x:500:500:rocrocket,China:/home/rocrocket:/bin/zsh
```

You can see that the last part of the output has changed to `/bin/zsh`. The next time you log in, Linux will read this command to start the shell.

**Change the shell back to /bin/bash:**

```shell
[rocrocket@localhost ~]$ chsh -s /bin/bash
Changing shell for rocrocket.
Password:
Shell changed.
```
