netstat
===

Display network system status in Linux

## Description

The **netstat command** is used to print information about the Linux network system, allowing you to understand the overall network status of the system.

### Syntax

```shell
netstat [options]
```

### Options

```shell
-a, --all: Display all active sockets.
-A <family>, --<family>: List sockets for the specified address family (e.g., inet, unix).
-c, --continuous: List network status continuously.
-C, --cache: Display routing cache information.
-e, --extend: Display extra information.
-F, --fib: Display Forwarding Information Base (FIB).
-g, --groups: Display multicast group membership information.
-h, --help: Display help message.
-i, --interfaces: Display network interface table.
-l, --listening: Display only listening sockets.
-M, --masquerade: Display masqueraded connections.
-n, --numeric: Show numerical addresses instead of hostnames.
-N, --netlink, --symbolic: Show symbolic names for network hardware peripherals.
-o, --timers: Display timers.
-p, --programs: Show PID and name of the program to which each socket belongs.
-r, --route: Display the kernel routing table.
-s, --statistics: Display statistics for each protocol.
-t, --tcp: Display TCP connections.
-u, --udp: Display UDP connections.
-v, --verbose: Verbose mode, show execution details.
-V, --version: Display version information.
-w, --raw: Display RAW protocol connections.
-x, --unix: Same as "-A unix".
--ip, --inet: Same as "-A inet".
```

### Examples

**List all ports (listening and non-listening)**

```shell
netstat -a     # List all ports
netstat -at    # List all TCP ports
netstat -au    # List all UDP ports
```

**List only listening sockets**

```shell
netstat -l        # Display only listening ports
netstat -lt       # List all listening TCP ports
netstat -lu       # List all listening UDP ports
netstat -lx       # List all listening UNIX sockets
```

**Display statistics for each protocol**

```shell
netstat -s    # Display statistics for all protocols
netstat -st   # Display statistics for TCP ports
netstat -su   # Display statistics for UDP ports
```

**Show PID and process name in output**

```shell
netstat -pt
```

`netstat -p` can be combined with other flags to add the "PID/Program name" to the output, which is very helpful for debugging.

**Do not resolve hostnames, ports, or usernames**

Use `netstat -n` when you don't want names to be displayed. This uses numbers instead and speeds up output by avoiding DNS/name lookups.

```shell
netstat -an
```

If you only want to hide specific types of names:

```shell
netstat -a --numeric-ports
netstat -a --numeric-hosts
netstat -a --numeric-users
```

**Continuous output**

```shell
netstat -c   # Output network information every second
```

**Display unsupported address families**

```shell
netstat --verbose
```

At the end of the output, you might see messages like:

```shell
netstat: no support for `AF IPX' on this system.
netstat: no support for `AF AX25' on this system.
```

**Display kernel routing information**

```shell
netstat -r
```

Use `netstat -rn` for numerical format.

**Find the port a program is using**

Note: Some processes may not be visible without root privileges.

```shell
netstat -ap | grep ssh
```

Find the process running on a specific port:

```shell
netstat -an | grep ':80'
```

**Find Process ID via port**

```bash
netstat -anp | grep 8081 | grep LISTEN | awk '{printf $7}' | cut -d/ -f1
```

**Display network interface list**

```shell
netstat -i
```

For detailed information similar to `ifconfig`, use `netstat -ie`.

**IP and TCP Analysis**

Find the IP addresses with the most connections to a specific port:

```shell
netstat -ntu | grep :80 | awk '{print $5}' | cut -d: -f1 | awk '{++ip[$1]} END {for(i in ip) print ip[i],"\t",i}' | sort -nr
```

List TCP states:

```shell
netstat -nt | grep -e 127.0.0.1 -e 0.0.0.0 -e ::: -v | awk '/^tcp/ {++state[$NF]} END {for(i in state) print i,"\t",state[i]}'
```

Check the number of `php-cgi` processes:

```shell
netstat -anpo | grep "php-cgi" | wc -l
```

## Extended Knowledge

### Network Connection States

There are 12 possible states, the first 11 correspond to the TCP three-way handshake and four-way handshake processes:

1.  **LISTEN**: The server is waiting for an incoming TCP connection request.
2.  **SYN_SENT**: The client has sent a SYN request and is waiting for a matching connection request.
3.  **SYN_RECV**: The server has received a SYN, sent its own SYN+ACK, and is waiting for the client's ACK.
4.  **ESTABLISHED**: The connection is open and data can be exchanged.
5.  **FIN_WAIT1**: The local end has initiated a close and is waiting for a connection termination request from the remote TCP or an acknowledgement of the previously sent termination request.
6.  **CLOSE_WAIT**: The remote end has initiated a close, and the local end is waiting for a connection termination request from the local user.
7.  **FIN_WAIT2**: The local end has received an ACK for its termination request and is waiting for a termination request from the remote TCP.
8.  **LAST_ACK**: The local end has sent its own termination request and is waiting for an ACK from the remote TCP.
9.  **TIME_WAIT**: The local end has received the remote end's termination request, sent an ACK, and is waiting to ensure the remote TCP received it.
10. **CLOSING**: Both ends have initiated a close simultaneously; waiting for termination request acknowledgement from the remote TCP.
11. **CLOSED**: No connection exists.
12. **UNKNOWN**: Unknown socket state.

### Common Flags

*   **SYN**: (Synchronize) Used during the three-way handshake to establish a new connection.
*   **ACK**: (Acknowledgement) Used to confirm receipt of data or requests.
*   **FIN**: (Finish) Used to terminate a session.
