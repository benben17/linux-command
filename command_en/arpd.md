arpd
===

Collect gratuitous ARP information

## Additional Information

The **arpd command** is a daemon used to collect gratuitous ARP information. It saves the collected information on the disk or provides it to kernel users when needed to avoid redundant broadcasts.

### Syntax

```shell
arpd (options) (parameters)
```

### Options

```shell
-l: Output the ARP database to the standard output device and exit.
-f: Specify a text file to read and load the arpd database; the file format is similar to the output of "-l".
-b: Specify the arpd database file; the default location is "/var/lib/arpd.db".
-a: Specify the number of queries before a target is considered dead.
-k: Prohibit sending broadcast queries through the kernel.
-n: Set the buffer expiration time.
```

### Parameters

Network interface: Specifies the network interface.

### Examples

Start the arpd process:

```shell
arpd -b /var/tmp/arpd.db
```

View the results after running for a while:

```shell
arpd -l -b /var/tmp/arpd.db
```
