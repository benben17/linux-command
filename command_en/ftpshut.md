ftpshut
===

Shut down the FTP server at a specified time.

## Description

The `ftpshut` command allows a system administrator to shut down the FTP server at a scheduled time and issue warning messages to notify users before the shutdown occurs. If the shutdown time is set to "none," the server will shut down immediately. If a format like "+30" is used, the server will shut down in 30 minutes. Similarly, using the "1130" format means the server will shut down at 11:30 AM daily (using a 24-hour clock). After the FTP server is shut down, a file named `shutmsg` is created in the `/etc` directory. Deleting this file will re-enable the FTP server.

### Syntax

```shell
ftpshut [-d <minutes>] [-l <minutes>] [shutdown-time] ["warning-message"]
```

### Parameters

```shell
-d <minutes>   Time to disconnect all active FTP connections.
-l <minutes>   Time to stop accepting new FTP logins.
```
