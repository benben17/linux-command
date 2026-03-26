login
===

Log into the system or switch user identity

## Description

The **login** command is used to provide a login interface for re-logging or switching user identities. In distributions like Slackware, you can append the username after the command, and it will prompt for the password. When the `/etc/nologin` file exists, only the root account can log into the system; other users are denied access.

### Syntax

```shell
login (options) (parameters)
```

### Options

```shell
-p: Tell the login command not to destroy environment variables;
-h: Specify the hostname of the remote server.
```

### Parameters

Username: Specify the username to log in as.
