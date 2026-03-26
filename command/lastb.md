lastb
===

List information about users who failed to log into the system

## Description

The **lastb** command is used to display a list of failed login attempts, which can help identify abnormal login activity on the system. When executed alone, it reads the `btmp` file located in the `/var/log` directory and displays all records of failed login attempts stored in that file.

### Syntax

```shell
lastb (options) (parameters)
```

### Options

```shell
-a: Display the hostname or IP address from which the login attempt was made at the end of the line;
-d: Convert IP addresses into hostnames;
-f <file>: Specify an alternative log file;
-n <number> or -<number>: Set the number of lines to display;
-R: Do not display the hostname or IP address of the login attempt;
-x: Display system shutdown, reboot, and runlevel change information.
```

### Parameters

*   Username: Display the login list for the specified user;
*   Terminal: Display the login list for the specified terminal.

### Examples

Running the `lastb` command for the first time might result in the following error:

```shell
lastb: /var/log/btmp: No such file or directory
Perhaps this file was removed by the operator to prevent logging lastb info.
```

You simply need to create the missing file:

```shell
touch /var/log/btmp
```

Note that failed SSH login attempts might not be recorded in the `btmp` file depending on the configuration.

```shell
lastb | head
root     ssh:notty    110.84.129.3     Tue Dec 17 06:19 - 06:19  (00:00)
root     ssh:notty    110.84.129.3     Tue Dec 17 04:05 - 04:05  (00:00)
root     ssh:notty    110.84.129.3     Tue Dec 17 01:52 - 01:52  (00:00)
root     ssh:notty    110.84.129.3     Mon Dec 16 23:38 - 23:38  (00:00)
leonob   ssh:notty    222.211.85.18    Mon Dec 16 22:18 - 22:18  (00:00)
leonob   ssh:notty    222.211.85.18    Mon Dec 16 22:18 - 22:18  (00:00)
root     ssh:notty    110.84.129.3     Mon Dec 16 21:25 - 21:25  (00:00)
root     ssh:notty    110.84.129.3     Mon Dec 16 19:12 - 19:12  (00:00)
root     ssh:notty    110.84.129.3     Mon Dec 16 17:00 - 17:00  (00:00)
admin    ssh:notty    129.171.193.99   Mon Dec 16 16:52 - 16:52  (00:00)
```
