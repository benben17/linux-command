reject
===

Instructs the printing system to reject print jobs sent to the specified destination printer.

## Description

The **reject command** is part of the CUPS suite and is used to instruct the printing system to reject print jobs sent to the specified destination printer.

### Syntax

```shell
reject(options)(parameters)
```

### Options

```shell
-E: Force encryption when connecting to the server;
-U: Specify the username to use when connecting to the server;
-h: Specify the connection server name and port number;
-r: Specify the reason for rejecting the print job.
```

### Parameters

Destination: Specifies the target printer.
