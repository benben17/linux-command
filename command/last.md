last
===

List information about currently and previously logged-in users

## Description

The **last** command is used to display information about the most recent logins of users. When executed alone, it reads the `/var/log/wtmp` file and displays all the records of users who have logged into the system.

### Syntax

```shell
last (options) (parameters)
```

### Options

```shell
-a: Display the hostname or IP address from which the user logged in at the end of the line;
-d: Convert IP addresses into hostnames;
-f <file>: Specify an alternative log file;
-n <number> or -<number>: Set the number of lines to display;
-R: Do not display the hostname or IP address of the login;
-x: Display system shutdown, reboot, and runlevel change information.
```

### Parameters

*   Username: Display the login list for the specified user;
*   Terminal: Display the login list for the specified terminal.

### Examples

The `last` command is used to show user login status. Below is an example of displaying a fixed number of records:

```shell
last -10
root     pts/0        221.6.45.34      Tue Dec 17 09:40   still logged in
root     pts/0        221.6.45.34      Mon Dec 16 09:00 - 11:57  (02:56)
root     pts/0        222.94.97.122    Sun Dec 15 20:39 - 23:28  (02:48)
root     pts/0        222.95.209.80    Sat Dec 14 14:39 - 14:58  (00:18)
root     pts/0        221.6.45.34      Thu Dec 12 16:55 - 17:37  (00:41)
root     pts/0        49.65.139.195    Wed Dec 11 20:40 - 21:16  (00:35)
root     pts/0        49.65.139.195    Wed Dec 11 19:46 - 20:03  (00:17)
root     pts/0        221.6.45.34      Tue Dec 10 14:41 - 15:52  (01:10)
root     pts/0        221.6.45.34      Mon Dec  9 17:24 - 17:30  (00:06)
root     pts/0        221.6.45.34      Mon Dec  9 09:38 - 11:41  (02:02)
```
