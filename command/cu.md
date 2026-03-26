cu
===

Used to connect to another system host

## Supplemental Information

The **cu command** is used to connect to another system host. cu (call up) can connect to another host and work using an interface similar to a dial-up terminal, and can also perform simple file transfer tasks.

### Syntax

```shell
cu [dehnotv][-a<communication port>][-c<phone number>][-E<escape character>][-I<configuration file>][-l<peripheral device ID>]
[-s<connection speed>][-x<debug mode>][-z<system host>][--help][-nostop][--parity=none][<system host>/<phone number>]
```

### Options

```shell
-a <communication port> or -p <communication port> or --port <communication port> Use the specified communication port for connection.
-c <phone number> or --phone <phone number> Dial the phone number.
-d Enter debug mode.
-e or --parity=even Use even parity check.
-E <escape character> or --escape <escape character> Set the escape character.
-h or --halfduple Use half-duplex mode.
-I <configuration file> or --config <configuration file> Specify the configuration file to use.
-l <peripheral device ID> or --line <peripheral device ID> Specify a peripheral device as the connection device.
-n or --prompt Wait for the user to enter the phone number when dialing.
-o or --parity=odd Use odd parity check.
-s <connection speed> or --speed <connection speed> or --baud <connection speed> or -<connection speed> Set the connection speed in baud rate.
-t or --maper Replace CR character with LF+CR character.
-v or --version Display version information.
-x <debug mode> or --debug <debug mode> Use debug mode.
-z <system host> or --system <system host> Connect to the system host.
--help Online help.
--nostop Turn off Xon/Xoff software flow control.
--parity=none Do not use parity check.
```

### Examples

Connect to a remote host:

```shell
cu -c 0102377765
cu -s 38400 9=12015551234
```
