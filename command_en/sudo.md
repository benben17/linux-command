sudo
===

Execute a command as another user

## Description

The **sudo command** (short for "superuser do") allows a permitted user to execute a command as another user, defaults to the root user. Permitted users are configured in the `/etc/sudoers` file. If an unauthorized user attempts to use `sudo`, a warning email is sent to the administrator. Users must enter their password, which then remains valid for 5 minutes (by default) before needing to be re-entered.

### Syntax 

```shell
sudo (options) (parameters)
```

### Options 

```shell
-b: Execute the command in the background.
-E: Inherit the current environment variables.
-h: Display help.
-H: Set the HOME environment variable to the HOME of the target user.
-k: Invalidate the password timeout, forcing a password prompt for the next sudo command.
-l: List the commands the current user is allowed or forbidden to run.
-p: Change the password prompt.
-s <shell>: Execute the specified shell.
-u <user>: Execute the command as the specified user. Defaults to root if not specified.
-v: Extend the password timeout by another 5 minutes.
-V: Display version information.
```

### Parameters 

Command: The command to run and its corresponding arguments.

### Examples 

```shell
$ sudo su -
# env | grep -E '(HOME|SHELL|USER|LOGNAME|^PATH|PWD|TEST_ETC|TEST_ZSH|TEST_PRO|TEST_BASH|TEST_HOME|SUDO)'
```

This command is equivalent to logging into a shell as the root superuser. The password used is that of the current user. Crucially, this command **reloads system configuration files like /etc/profile and /etc/bashrc, as well as the configuration files corresponding to the root user's $SHELL environment variable** (e.g., /root/.bashrc for bash or /root/.zshrc for zsh), resulting in a complete root environment.

```shell
$ sudo -i
# env | grep -E '(HOME|SHELL|USER|LOGNAME|^PATH|PWD|TEST_ETC|TEST_ZSH|TEST_PRO|TEST_BASH|TEST_HOME|SUDO)'
```

This command is essentially the same as `sudo su -`, providing a root environment, but it retains some information from the current user.

```shell
$ sudo -s
# env | grep -E '(HOME|SHELL|USER|LOGNAME|^PATH|PWD|TEST_ETC|TEST_ZSH|TEST_PRO|TEST_BASH|TEST_HOME|SUDO)' --color
```

This command **starts a non-login shell for the root superuser using the current user's $SHELL, without loading system configurations like /etc/profile**. Therefore, environment variables defined in /etc/profile (like TEST_ETC) will not be visible. However, it will **load the configuration files for the root user**. After execution, the current user's directory is not changed.

Configuring `sudo` must be done by editing the `/etc/sudoers` file, which only the superuser can modify, and it must be edited using `visudo`. `visudo` is used for two reasons: it prevents simultaneous edits by multiple users and performs limited syntax checking. Even if you are the only superuser, it is best to use `visudo` to verify syntax.

By default, `visudo` opens the configuration file in `vi`. It will not save a configuration file with syntax errors; instead, it will alert you to the problem and ask how to proceed:

```shell
>>> sudoers file: syntax error, line 22 <<
```

You have three options: "e" to re-edit, "x" to exit without saving, or "Q" to quit and save. If you choose "Q", `sudo` will not run until the error is corrected.

Let's look at how to write the configuration file. For example, to allow user `foobar` to execute all root commands via `sudo`, open the file with `visudo` as root:

```shell
# Runas alias specification
# User privilege specification
root    ALL=(ALL) ALL
```

Add a line for `foobar` (preferably using tabs for spacing):

```shell
foobar ALL=(ALL) ALL
```

After saving and exiting, switch to `foobar` and run a command:

```shell
[foobar@localhost ~]$ ls /root
ls: /root: Permission denied

[foobar@localhost ~]$ sudo ls /root
PassWord:
anaconda-ks.cfg Desktop install.log install.log.syslog
```

To restrict `foobar`'s permissions so they can only use `ls` and `ifconfig` as root, change the line to:

```shell
foobar localhost= /sbin/ifconfig, /bin/ls
```

Now execute:

```shell
[foobar@localhost ~]$ sudo head -5 /etc/shadow
Password:
Sorry, user foobar is not allowed to execute '/usr/bin/head -5 /etc/shadow' as root on localhost.localdomain.

[foobar@localhost ~]$ sudo /sbin/ifconfig eth0 Link encap:Ethernet HWaddr 00:14:85:EC:E9:9B...
```

The three `ALL` terms mean:
1. The hosts in the network.
2. The target user (whom to execute as).
3. The command names.

To allow `foobar` to execute `kill` as `jimmy` or `rene` on the `linux` host:

```shell
foobar linux=(jimmy,rene) /bin/kill
```

Use `sudo -u jimmy kill PID` or `sudo -u rene kill PID`. To avoid using `-u` every time, set a default target user:

```shell
Defaults:foobar runas_default=rene
```

To avoid entering a password for certain commands:

```shell
foobar localhost=NOPASSWD: /bin/cat, /bin/ls
```

Using the `!` operator to exclude commands is generally not recommended as users can often bypass this by copying and renaming the command.

**Logging and Security**

`sudo` can record logs and report to system administrators. To enable logging:

```shell
touch /var/log/sudo
vi /etc/syslog.conf
```

Add the following to `syslog.conf` (separated by a tab) and save:

```shell
local2.debug                    /var/log/sudo
```

Restart the syslog daemon:

```shell
ps aux | grep syslogd
kill -HUP <PID>
```

`sudo` will now write logs:

```shell
[foobar@localhost ~]$ sudo ls /root
...
$ cat /var/log/sudo
Jul 28 22:52:54 localhost sudo: foobar : TTY=pts/1 ; pwd=/home/foobar ; USER=root ; command=/bin/ls /root
```

Note that shell redirections (e.g., `sudo cat /etc/shadow > /dev/null`) are not recorded because the shell handles redirection before `sudo` executes the command. `sudo` also protects security by not passing certain environment variables (like PATH, HOME, SHELL) to the command unless configured in `sudoers`.
