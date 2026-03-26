sftp
===

An interactive file transfer program.

## Description

The **sftp command** is an interactive file transfer program. Its usage and operation are similar to the `ftp` command, but `sftp` encrypts all transmitted information using SSH. It also supports features like public key authentication and compression.

### Syntax

```shell
sftp [options] [parameters]
```

### Options

```shell
-B: Specify the buffer size used for file transfers.
-l: Use SSH protocol version 1.
-b: Specify a batch file containing commands to be executed.
-C: Enable compression.
-o: Specify SSH options.
-F: Specify an alternative SSH configuration file.
-R: Specify the number of requests that can be outstanding at any one time.
-v: Increase the logging level.
```

### Parameters

Target Host: Specify the IP address or hostname of the SFTP server.

### Examples

Establish a connection:

```shell
$ sftp username@1.1.1.1 # Press Enter and provide the password
```

Download a file to a specified path:

```shell
sftp> get /export/sftp/test.csv /Users/my/Downloads
Fetching /export/sftp/test.csv to /Users/my/Downloads/test.csv
/export/sftp/test.csv            100%  133     0.3KB/s   00:00
```

Upload a local file to a specified path on the server:

```shell
sftp> put /Users/my/Downloads/re-produce.gif /export/sftp
Uploading /Users/my/Downloads/re-produce.gif to /export/sftp/re-produce.gif
/Users/my/Downloads/re-produce.gif            100%  257KB  86.6KB/s   00:02
```
