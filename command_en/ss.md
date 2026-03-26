ss
===

Socket statistics tool, part of the iproute2 package. It allows you to query detailed socket statistics and is a more modern and faster alternative to `netstat`.

## Description

The **ss command** is used to display information about active sockets. It can retrieve socket statistics and display information similar to `netstat`, but it is faster and more efficient. `ss` can display more detailed information about TCP and connection states.

When the number of socket connections on a server is very large, `netstat` or `cat /proc/net/tcp` can be very slow. `ss` is much faster because it utilizes `tcp_diag` in the TCP protocol stack, which allows it to get information directly from the Linux kernel. If `tcp_diag` is not available, `ss` will still work but will be slightly slower.

### Syntax

```shell
ss [parameter]
ss [parameter] [filter]
```

### Options

```shell
-h, --help      Display help information
-V, --version   Display program version information
-n, --numeric   Do not resolve service names
-r, --resolve   Resolve hostnames
-a, --all       Show all sockets
-l, --listening Show listening sockets
-o, --options   Show timer information
-e, --extended  Show detailed socket information
-m, --memory    Show socket memory usage
-p, --processes Show processes using the socket
-i, --info      Show internal TCP information
-s, --summary   Show socket usage summary
-4, --ipv4      Display only IPv4 sockets
-6, --ipv6      Display only IPv6 sockets
-0, --packet    Display PACKET sockets
-t, --tcp       Display only TCP sockets
-u, --udp       Display only UDP sockets
-d, --dccp      Display only DCCP sockets
-w, --raw       Display only RAW sockets
-x, --unix      Display only Unix domain sockets
-f, --family=FAMILY  Display sockets of type FAMILY (unix, inet, inet6, link, netlink)
-A, --query=QUERY, --socket=QUERY
      QUERY := {all|inet|tcp|udp|raw|unix|packet|netlink}[,QUERY]
-D, --diag=FILE     Dump raw TCP socket information to a file
-F, --filter=FILE  Read filter information from a file
       FILTER := [ state TCP-STATE ] [ EXPRESSION ]
```

### Examples

```shell
ss -t -a    # Show all TCP connections
ss -s       # Show socket summary
ss -l       # List all listening ports
ss -pl      # Show processes using sockets
ss -lp | grep 3306  # Find the application using port 3306
ss -u -a    # Show all UDP sockets
ss -o state established '( dport = :smtp or sport = :smtp )' # Show all established SMTP connections
ss -o state established '( dport = :http or sport = :http )' # Show all established HTTP connections
ss -o state fin-wait-1 '( sport = :http or sport = :https )' dst 193.233.7/24  # List TCP sockets in FIN-WAIT-1 state with source port 80 or 443 and target network 193.233.7/24

# Efficiency comparison between ss and netstat
time netstat -at
time ss

# Matching remote address and port
# ss dst ADDRESS_PATTERN
ss dst 192.168.1.5
ss dst 192.168.119.113:http
ss dst 192.168.119.113:smtp
ss dst 192.168.119.113:443

# Matching local address and port
# ss src ADDRESS_PATTERN
ss src 192.168.119.103
ss src 192.168.119.103:http
ss src 192.168.119.103:80
ss src 192.168.119.103:smtp
ss src 192.168.119.103:25
```

**Compare local or remote ports with a value:**

```shell
# ss dport OP PORT: Compare remote port with a value
# ss sport OP PORT: Compare local port with a value
# OP can be one of the following:
# <= or le : less than or equal to
# >= or ge : greater than or equal to
# == or eq : equal to
# != or ne : not equal to
# < or gt : greater than (Note: Chinese text had < or gt, but usually < is lt and > is gt)
# > or lt : less than
ss  sport = :http
ss  dport = :http
ss  dport \> :1024
ss  sport \> :1024
ss sport \< :32000
ss  sport eq :22
ss  dport != :22
ss  state connected sport = :http
ss \( sport = :http or sport = :https \)
ss -o state fin-wait-1 \( sport = :http or sport = :https \) dst 192.168.1/24
```

**Filter Sockets by TCP State:**

```shell
ss -4 state closing
# ss -4 state FILTER-NAME-HERE
# ss -6 state FILTER-NAME-HERE
# FILTER-NAME-HERE can be:
# established, syn-sent, syn-recv, fin-wait-1, fin-wait-2, time-wait, closed, close-wait, last-ack, listen, closing
# all: All of the above
# connected: All states except listen and closed
# synchronized: All connected states except syn-sent
# bucket: Sockets maintained as minisockets (e.g., time-wait and syn-recv)
# big: Opposite of bucket
```

**Display TCP Connections:**

```shell
[root@localhost ~]# ss -t -a
State       Recv-Q Send-Q                            Local Address:Port                                Peer Address:Port
LISTEN      0      0                                             *:3306                                           *:*
LISTEN      0      0                                             *:http                                           *:*
LISTEN      0      0                                             *:ssh                                            *:*
LISTEN      0      0                                     127.0.0.1:smtp                                           *:*
ESTAB       0      0                                112.124.15.130:42071                              42.156.166.25:http
ESTAB       0      0                                112.124.15.130:ssh                              121.229.196.235:33398
```

**Show Socket Summary:**

```shell
[root@localhost ~]# ss -s
Total: 172 (kernel 189)
TCP:   10 (estab 2, closed 4, orphaned 0, synrecv 0, timewait 0/0), ports 5

Transport Total     ip        IPv6
*         189       -         -
RAW       0         0         0
UDP       5         5         0
TCP       6         6         0
INET      11        11        0
FRAG      0         0         0
```

**List all listening ports:**

```shell
[root@localhost ~]# ss -l
Recv-Q Send-Q                                 Local Address:Port                                     Peer Address:Port
0      0                                                  *:3306                                                *:*
0      0                                                  *:http                                                *:*
0      0                                                  *:ssh                                                 *:*
0      0                                          127.0.0.1:smtp                                                *:*
```

**Show processes using sockets:**

```shell
[root@localhost ~]# ss -pl
Recv-Q Send-Q                                          Local Address:Port                                              Peer Address:Port
0      0                                                           *:3306                                                         *:*        users:(("mysqld",1718,10))
0      0                                                           *:http                                                         *:*        users:(("nginx",13312,5),("nginx",13333,5))
0      0                                                           *:ssh                                                          *:*        users:(("sshd",1379,3))
0      0                                                   127.0.0.1:smtp                                                         *:*        us
```

**Find the application for a specific port:**

```shell
[root@localhost ~]# ss -pl | grep 3306
0      0                            *:3306                          *:*        users:(("mysqld",1718,10))
```

**Show all UDP Sockets:**

```shell
[root@localhost ~]# ss -u -a
State       Recv-Q Send-Q                                     Local Address:Port                                         Peer Address:Port
UNCONN      0      0                                                      *:syslog                                                  *:*
UNCONN      0      0                                         112.124.15.130:ntp                                                     *:*
UNCONN      0      0                                            10.160.7.81:ntp                                                     *:*
UNCONN      0      0                                              127.0.0.1:ntp                                                     *:*
UNCONN      0      0                                                      *:ntp                                                     *:*
```

**Show all connections on port 22 (SSH):**

```shell
[root@localhost ~]# ss state all sport = :ssh
Netid State      Recv-Q Send-Q     Local Address:Port                      Peer Address:Port
tcp   LISTEN     0      128                    *:ssh                                  *:*
tcp   ESTAB      0      0          192.168.0.136:ssh                      192.168.0.102:46540
tcp   LISTEN     0      128                   :::ssh                                 :::*
```

**Check TCP connection states:**

```shell
[root@localhost ~]# ss -tan | awk 'NR>1{++S[$1]}END{for (a in S) print a,S[a]}'
LISTEN 7
ESTAB 31
TIME-WAIT 28
```
