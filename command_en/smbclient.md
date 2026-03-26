smbclient
===

Interactive access to Samba servers.

## Description

The **smbclient command** is part of the Samba suite. It provides a command-line interface to interactively access shared resources on a Samba server.

### Syntax

```shell
smbclient [option] [parameter]
```

### Options

```shell
-B <IP address>: The IP address used when sending broadcast packets;
-d <debug level>: Specify the detail level of events recorded in the log file;
-E: Send messages to standard error output;
-h: Display help;
-i <scope>: Set the NetBIOS name scope;
-I <IP address>: Specify the server's IP address;
-l <log file>: Specify the name of the log file;
-L: List all resources shared by the server;
-M <NetBIOS name>: Send messages to the specified host using the WinPopup protocol;
-n <NetBIOS name>: Specify the NetBIOS name the client will use;
-N: Do not ask for a password;
-O <socket options>: Set client-side TCP socket options;
-p <TCP port>: Specify the server's TCP port number;
-R <name resolve order>: Set the order of NetBIOS name resolution;
-s <directory>: Specify the directory where smb.conf is located;
-t <terminal code>: Set which character code to use for parsing filenames on the server;
-T <tar options>: Back up all shared files on the server into a tar format file;
-U <username>: Specify the username;
-w <workgroup>: Specify the workgroup name.
```

### Parameters

SMB server: Specify the SMB server to connect to.

### Examples

**List shared folders provided by a specific IP address:**

```shell
smbclient -L 192.168.0.1 -U username%password
```

**Use smbclient like an FTP client:**

```shell
smbclient //192.168.0.1/tmp -U username%password
```

After successfully executing the `smbclient` command, you will enter the smbclient environment with the prompt: `smb:/>`

Many commands here are similar to FTP commands, such as `cd`, `lcd`, `get`, `mget`, `put`, `mput`, etc. These commands allow you to access shared resources on the remote host.

**Execute a command directly without entering interactive mode:**

```shell
smbclient -c "ls" //192.168.0.1/tmp -U username%password
```

This is equivalent to:

```shell
smbclient //192.168.0.1/tmp -U username%password
smb:/>ls
```

**Create a shared folder:**

```shell
smbclient -c "mkdir share1" //192.168.0.1/tmp -U username%password
```

If the share `//192.168.0.1/tmp` is read-only, it will return: `NT_STATUS_ACCESS_DENIED making remote directory /share1`
