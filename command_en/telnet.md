telnet
===

Login to remote hosts and manage (test IP port connectivity)

## Description

The **telnet command** is used to log in to remote hosts and manage them. Because telnet uses cleartext to transmit messages, its security is poor. Many Linux servers do not enable the telnet service, opting instead for the more secure SSH method. However, many other systems may still use telnet to provide remote login, so it is still necessary to understand how to use the telnet client.

### Syntax

```shell
telnet [options] [parameters]
```

### Options

```shell
-8: Allow the use of 8-bit character data, including input and output;
-a: Attempt automatic login to the remote system;
-b<host alias>: Use an alias to specify the remote host name;
-c: Do not read the .telnetrc file in the user's home directory;
-d: Enable debugging mode;
-e<escape character>: Set the escape character;
-E: Filter out the escape character;
-f: This parameter has the same effect as specifying the "-F" parameter;
-F: When using Kerberos V5 authentication, adding this parameter can upload the local host's authentication data to the remote host;
-k<domain name>: When using Kerberos authentication, adding this parameter makes the remote host use the specified realm name instead of the host's domain name;
-K: Do not automatically log in to the remote host;
-l<username>: Specify the username to log in to the remote host;
-L: Allow the output of 8-bit character data;
-n<record file>: Specify a file to record relevant information;
-r: Use a user interface similar to the rlogin command;
-S<service type>: Set the IP TOS information required for the telnet connection;
-x: Use data encryption if the host supports it;
-X<auth type>: Disable the specified authentication type.
```

### Parameters

*   Remote Host: Specifies the remote host to log in to for management;
*   Port: Specifies the port number used by the TELNET protocol.

### Examples

```shell
$ telnet 192.168.2.10
Trying 192.168.2.10...
Connected to 192.168.2.10 (192.168.2.10).
Escape character is '^]'.

    localhost (Linux release 2.6.18-274.18.1.el5 #1 SMP Thu Feb 9 12:45:44 EST 2012) (1)

login: root
Password:
Login incorrect
```

Generally, root is not allowed to log in remotely. You can log in with a regular account first and then switch to the root user using `su -`.

```shell
$ telnet 192.168.188.132
Trying 192.168.188.132...
telnet: connect to address 192.168.188.132: Connection refused
telnet: Unable to connect to remote host
```

Troubleshooting this situation:

1. Confirm if the IP address is correct.
2. Confirm if the host corresponding to the IP address is powered on.
3. If the host has started, confirm if the routing settings are correct (use the `route` command).
4. If the host has started, confirm if the telnet service is enabled on the host (use the `netstat` command to see if there is a LISTEN status row for TCP port 23).
5. If the host has started the telnet service, confirm if the firewall has opened access to port 23 (use `iptables-save`).

**Start the telnet service**

```shell
service xinetd restart
```

Configuration parameters, usually as follows:

```shell
service telnet
{
    disable = no # Enable
    flags = REUSE # Socket reusable
    socket_type = stream # Connection method is TCP
    wait = no # Start a process for each request
    user = root # User starting the service is root
    server = /usr/sbin/in.telnetd # Process to be activated
    log_on_failure += USERID # Record login username on failure
}
```

To configure a list of allowed clients, add:
```
only_from = 192.168.0.2 # Only allow 192.168.0.2 to log in
```
To configure a list of forbidden clients, add:
```
no_access = 192.168.0.{2,3,4} # Forbid 192.168.0.2, 192.168.0.3, 192.168.0.4 from logging in
```
To set open periods, add:
```
access_times = 9:00-12:00 13:00-17:00 # Service open only during these two periods daily
```

If you have two IP addresses, one private (e.g., 192.168.0.2) and one public (e.g., 218.75.74.83), and you want users to only log in from the private network, add:
```
bind = 192.168.0.2
```

Specific meanings and syntax of each configuration item can be found in the xinetd configuration file property description (`man xinetd.conf`).

Configure the port by modifying the services file:

```shell
# vi /etc/services
```

Find the following two lines:

```shell
telnet 23/tcp
telnet 23/udp
```

If there is a `#` character in front, remove it. The default port for telnet is 23, which is a major target for hacker port scans. Therefore, it's best to change this port. The method is simple: change the number 23 to a larger number, such as 61123. Note that port numbers below 1024 are reserved by the internet and should ideally not be used. Also, ensure the port does not conflict with other services.

Restart the service:
```
service xinetd restart
```
