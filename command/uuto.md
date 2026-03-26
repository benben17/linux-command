uuto
===

Send files to a remote UUCP host.

## Description

The **uuto command** is a script file that actually executes uucp to send files to a remote UUCP host and notifies the user on the remote host via email once the task is complete.

### Syntax

```shell
uuto [file] [destination]
```

### Examples

Send a file to the `tmp` directory of the remote UUCP host `localhost`. Enter the following command directly at the command prompt:

```shell
uuto ./testfile localhost/tmp # Send file to the tmp directory of remote UUCP host localhost
```

Note: This command typically produces no output.
