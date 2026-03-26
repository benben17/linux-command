ftp
===

Client for the File Transfer Protocol.

## Description

The **ftp command** is the interface to the File Transfer Protocol. It is used to transfer files between a local machine and a remote host. Mastering `ftp` commands makes remote file management much easier.

### Syntax

```shell
ftp (options) (parameters)
```

### Options

```shell
-d: Enable debugging (verbose output).
-i: Disable interactive prompting during multiple file transfers.
-g: Disable filename globbing (special character expansion).
-n: Restrain ftp from attempting "auto-login" upon initial connection.
-v: Verbose mode; show all responses from the remote server.
```

### Parameters

Host: The hostname or IP address of the remote FTP server.

### Examples

```shell
ftp> ascii  # Set file transfer type to ASCII (default).
ftp> bell   # Sound a bell after each file transfer is completed.
ftp> binary # Set file transfer type to binary.
ftp> bye    # Terminate the FTP session and exit.
ftp> case   # Toggle local filename case mapping (for mget).
ftp> cd     # Change directory on the remote machine.
ftp> cdup   # Change to the parent directory on the remote machine.
ftp> chmod  # Change permissions of a file on the remote machine.
ftp> close  # Terminate the FTP session but stay in the ftp shell.
ftp> delete # Delete a file on the remote machine.
ftp> dir [remote-directory] [local-file] # List files in the remote directory.
ftp> get [remote-file] [local-file] # Transfer a file from remote to local.
ftp> help [command] # Display help for a command.
ftp> lcd # Change working directory on the local machine.
ftp> ls [remote-directory] [local-file] # List remote files (shorthand for dir).
ftp> macdef                 # Define a macro.
ftp> mdelete [remote-files] # Delete multiple files on the remote machine.
ftp> mget [remote-files]    # Transfer multiple files from remote to local.
ftp> mkdir directory-name   # Create a directory on the remote machine.
ftp> mput local-files # Transfer multiple files from local to remote.
ftp> open host [port] # Open a connection to a remote host.
ftp> prompt           # Toggle interactive prompting.
ftp> put local-file [remote-file] # Transfer a file from local to remote.
ftp> pwd  # Print the current working directory on the remote machine.
ftp> quit # Same as bye.
ftp> recv remote-file [local-file] # Same as get.
ftp> rename [from] [to]     # Rename a file on the remote machine.
ftp> rmdir directory-name   # Remove a directory on the remote machine.
ftp> send local-file [remote-file] # Same as put.
ftp> status   # Show the current status of the FTP session.
ftp> system   # Show the remote system type.
ftp> user user-name [password] [account] # Login as a different user.
ftp> ? [command] # Same as help.
ftp> ! # Escape to the local shell.
```

Anonymous Login Credentials:

```shell
Username: anonymous
Password: anonymous@
```

Closing Connection:

```shell
bye
exit
quit
```

Downloading Files:

```shell
ftp> get readme.txt # Download a single file.
ftp> mget *.txt     # Download multiple files.
```

Uploading Files:

```shell
ftp> put /path/readme.txt # Upload a single file.
ftp> mput *.txt           # Upload multiple files.
```
