sh
===

Shell command interpreter.

## Description

The **sh command** is a shell command language interpreter that reads commands from standard input or a file. It acts as an interface between user input and the kernel. Bourne Again Shell (bash), developed by the Free Software Foundation (GNU), is the default shell on many Linux systems. Bash is compatible with the original Bourne Shell and incorporates features from C Shell and Korn Shell.

### Syntax

```shell
bash [options] [file]
```

### Options

```shell
-c string: Read commands from the specified string following the -c option.
-i: Run the shell in interactive mode.
-n: Perform syntax checking on a shell script without executing it.
-x: Enable tracing of shell script execution, printing each command before it is run.
```

### Examples

Use the `-x` option to trace and debug a shell script, printing each line executed along with its current state:

```shell
[root@AY1307311912260196fcZ satools]# sh -x check_ssh_login.sh
+ DEFINE=30
+ cat /var/log/secure
+ awk '/Failed/ {++ip[$(NF-3)]} END {for (i in ip) print i"="ip[i]}'
++ cat /root/satools/black.txt
+ for i in '`cat /root/satools/black.txt`'
++ echo 121.42.0.16=1427
++ awk -F= '{print $1}'
+ IP=121.42.0.16
++ echo 121.42.0.16=1427
++ awk -F= '{print $2}'
+ NUM=1427
+ '[' 1427 -gt 30 ']'
+ grep 121.42.0.16 /etc/hosts.deny
+ '[' 1 -gt 0 ']'
+ echo sshd:121.42.0.16
+ echo vsftpd:121.42.0.16
+ for i in '`cat /root/satools/black.txt`'
++ echo 121.42.0.72=276
++ awk -F= '{print $1}'
+ IP=121.42.0.72
++ awk -F= '{print $2}'
++ echo 121.42.0.72=276
+ NUM=276
+ '[' 276 -gt 30 ']'
+ grep 121.42.0.72 /etc/hosts.deny
+ '[' 1 -gt 0 ']'
+ echo sshd:121.42.0.72
+ echo vsftpd:121.42.0.72
```
