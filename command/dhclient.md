dhclient
===

Dynamic Host Configuration Protocol (DHCP) client.

## Description

The **dhclient** command provides a means for configuring one or more network interfaces using the Dynamic Host Configuration Protocol.

### Syntax

```shell
dhclient (options) (parameters)
```

### Options

```shell
-p <port>  Specify the port number on which the DHCP client listens.
-d         Force dhclient to run as a foreground process.
-q         Quiet mode, suppress all terminal output except for error messages.
-r         Release the current lease and stop the running DHCP client.
```

### Parameters

Network Interface: The network interface to operate on.

### Examples

```shell
dhclient -r     # Release IP address
dhclient        # Obtain IP address
```
