lpadmin
===

Configure CUPS printers and classes

## Description

The **lpadmin** command is used to configure printers and classes in the CUPS suite. It is also used to set the default printer for the print server.

### Syntax

```shell
lpadmin (options) (parameters)
```

### Options

```shell
-c <class>: Add the printer to the specified class;
-i <interface>: Set a System V style interface script for the printer;
-m <model>: Set a standard System V interface script or PPD file from the model directory;
-o <option=value>: Set an option for the PPD or server;
-r <class>: Remove the printer from the specified class;
-u <allow/deny:user>: Set user-level access control for the printer;
-D <info>: Provide a textual description for the printer;
-E: Enable the printer to accept print jobs;
-L <location>: Provide a textual description of the printer's location;
-P <ppd-file>: Specify a PPD (PostScript Printer Description) file for the printer;
-p <printer>: Specify the name of the printer to configure;
-d <printer>: Set the default printer.
```

### Parameters

Printer: Specify the name of the printer to configure.
