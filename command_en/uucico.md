uucico
===

UUCP file transfer service program.

## Description

The **uucico command** is the UUCP file transfer service program. uucico is used to process file transfers sent to the queue by uucp or uux. uucico has two working modes: master mode and slave mode. In master mode, uucico calls the remote host; in slave mode, uucico accepts calls from the remote host.

### Syntax

```shell
uucico [-cCDefqvwz][-i<type>][-I<file>][-p<port>][-][-rl][-s<system>][-S<system>][-u<user>][-x<type>][--help]
```

### Options

```shell
-c or --quiet: Do not change the log file or update current status when no work is performed.
-C or --ifwork: Call the host specified by -s or -S only when there is work to be performed.
-D or --nodetach: Do not detach from the controlling terminal.
-e or --loop: Execute in slave mode and display a login prompt.
-f or --force: If an error occurs, call the host again without waiting.
-i<type> or --stdin<type>: Specify the connection port type when standard input is used.
-I<file> or --config<file>: Specify the configuration file to use.
-l or --prompt: Display a login prompt.
-p<port> or --port<port>: Specify the connection port number.
-q or --quiet: Do not start the uuxqt service program.
-r0 or --slave: Start in slave mode.
-s<system> or --system<system>: Call the specified host.
-u<user> or --login<user>: Specify the login user account, preventing arbitrary login accounts.
-v or --version: Display version information and exit.
-w or --wait: In master mode, display a login prompt when a call is performed.
-x<type> or -X<type> or --outgoing-debug<type>: Start the specified debug mode.
-z or --try-next: If execution fails, try the next option without ending the program.
--help: Display help and exit.
```

### Examples

Start the uucico service in master mode. Enter the following command directly at the command prompt:

```shell
uucico -r1
```

Note: This command generally produces no output.
