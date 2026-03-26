uupick
===

Handle incoming files transmitted via UUCP.

## Description

The **uupick command** handles incoming files. When other hosts transmit files via UUCP, the uupick command can be used to retrieve these files.

### Syntax

```shell
uupick [-v][-I<config_file>][-s<system>][-x<level>][--help]
```

### Options

```shell
-I<config_file> or --config<config_file>: Specify the configuration file.
-s<system> or --system<system>: Process files transmitted from the specified host.
-v or --version: Display version information.
--help: Display help information.
```

### Examples

Process files transmitted from the host `localhost`. Enter the following command directly at the command line:

```shell
uupick -s localhost
```

Note: This command typically produces no output.
