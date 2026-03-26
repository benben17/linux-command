rexec
===

Execute commands on a remote Linux system.

## Description

The **rexec command** is used to execute commands on a specified remote Linux host by sending an execution request to a remote rexec server.

The `rexec` command provides automatic login functionality by checking the `$HOME/.netrc` file (which contains the username and password used on the remote host). If no such entry is found or if the system is operating in a secure mode (see the `securetcpip` command), the `rexec` command prompts for a valid username and password for the remote host. In both cases, `rexec` causes `rexecd` on the remote system to use the default `compat` user login authentication method. `rexecd` does not look in the `/etc/security/user` file for alternative authentication methods. The `-n` flag can also be specified on the `rexec` command line to reset the automatic login feature.

### Syntax

```shell
rexec(options)(parameters)
```

### Options

```shell
-a: Standard error of the remote command is same as standard output; sending arbitrary signals to the remote process is not supported.
-l<username>: Specifies the username for connecting to the remote rexec server.
-p<password>: Specifies the password for connecting to the remote rexec server.
-n: Explicitly prompts for a username and password.
```

### Parameters

*   Remote host: Specifies the remote host (IP address or hostname).
*   Command: Specifies the command to be executed on the remote host.

### Examples

To execute the `date` command on a remote host, enter:

```shell
rexec host1 date
```

The output of the `date` command is now displayed on the local system. In this example, the `$HOME/.netrc` file on the local host contains a valid username and password for the remote host. If there is no valid entry in the `$HOME/.netrc` file for the remote host, you will be prompted for a login ID and password. After entering the required login information, the output of the `date` command is displayed on the local system.

To reset the automatic login feature and execute the `date` command on a remote host, enter:

```shell
rexec -nhost1 date
```

Enter the username and password when prompted; the output of the `date` command is now displayed on the local system.

To list the directory of another user on a remote host, enter:

```shell
rexec host1 ls -l /home/karen
```

The directory listing for user `karen` on the remote host `host1` is displayed on the local system.

If there is no valid entry in the `$HOME/.netrc` file for the remote host, you will be prompted for a login ID and password. After entering the required login information, the directory listing for user `karen` on the remote host `host1` is displayed on the local system.
