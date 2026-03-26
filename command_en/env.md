env
===

Display existing environment variables.

## Description

The **env** command is used to display the existing environment variables in the system and to execute commands in a modified environment. When the "-" option is used alone, it functions like "-i". If no options or parameters are provided, it simply displays the current environment variables.

If you use `env` to execute a command in a new environment, you might encounter a "no such file or directory" error because the `PATH` environment variable is not defined in the new environment. In such cases, you should redefine `PATH` or use absolute paths for the command.

### Syntax

```shell
env [options] [parameters]
```

### Options

```shell
-i: Start with an empty environment (ignore inherited environment).
-u <name>: Remove variable <name> from the current environment.
```

### Parameters

*   Variable Definitions: Define variables for the new environment, separated by spaces. Format: `NAME=VALUE`.
*   Command: Specify the command and its arguments to be executed.

### Examples

```shell
[root@localhost ~]# env
hostname=LinServ-1
TERM=linux
SHELL=/bin/bash
HISTSIZE=1000
SSH_CLIENT=192.168.2.111 2705 22
SSH_TTY=/dev/pts/0
USER=root
LS_COLORS=no=00:fi=00:di=01;34:ln=01;36:pi=40;33:so=01;35:bd=40;33;01:cd=40;33;01:or=01;05;37;41:mi=01;05;37;41:ex=01;32:*.cmd=01;32:*.exe=01;32:*.com=01;32:*.btm=01;32:*.bat=01;32:*.sh=01;32:*.csh=01;32:*.tar=01;31:*.tgz=01;31:*.arj=01;31:*.taz=01;31:*.lzh=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.gz=01;31:*.bz2=01;31:*.bz=01;31:*.tz=01;31:*.rpm=01;31:*.cpio=01;31:*.jpg=01;35:*.gif=01;35:*.bmp=01;35:*.xbm=01;35:*.xpm=01;35:*.png=01;35:*.tif=01;35:
mail=/var/spool/mail/root
PATH=/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
INPUTRC=/etc/inputrc
pwd=/root
LANG=zh_CN.UTF-8
SHLVL=1
HOME=/root
logname=root
SSH_CONNECTION=192.168.2.111 2705 192.168.2.2 22
LESSOPEN=|/usr/bin/lesspipe.sh %s
G_BROKEN_FILENAMES=1
_=/bin/env
```
