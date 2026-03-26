iperf
===

Network performance measurement tool.

## Description

`iperf` is a tool for measuring maximum TCP and UDP bandwidth performance. It can report bandwidth, delay jitter, and datagram loss. It is commonly used to test the performance of network devices like routers, firewalls, and switches.

There are two main versions: Unix/Linux and Windows (JPerf/XJPerf).

### Installation

For Linux:
```shell
tar -zxvf iperf-<version>.tar.gz
cd iperf-<version>
./configure
make
sudo make install
```

### Options

```bash
-f, --format [bkmaBKMA]   # Format bandwidth output (bits/sec, Bytes/sec, etc.).
-i, --interval n          # Set interval between periodic reports in seconds.
-l, --len n[KM]           # Set length of read/write buffer (TCP default 8KB, UDP 1470B).
-m, --print_mss           # Print TCP maximum segment size (MSS).
-p, --port n              # Set server port to listen on/connect to (default 5001).
-u, --udp                 # Use UDP instead of TCP.
-w, --window n[KM]        # Set socket buffer size (TCP window size).
-B, --bind host           # Bind to a specific interface or multicast address.
-C, --compatibility       # For use with older versions.
-M, --mss n               # Set TCP maximum segment size.
-N, --nodelay             # Set TCP no delay, disabling Nagle's Algorithm.
-V                        # Use IPv6.
```

**Server-specific Options:**
```bash
-s, --server              # Run in server mode.
-D                        # Run as a daemon.
-P n                      # Number of connections to handle before exiting.
```

**Client-specific Options:**
```bash
-b, --bandwidth n[KM]     # Set UDP target bandwidth (default 1 Mbit/sec).
-c, --client host         # Run in client mode, connecting to host.
-d, --dualtest            # Do a bidirectional test simultaneously.
-n, --num n[KM]           # Number of buffers to transmit (overrides -t).
-r, --tradeoff            # Do a bidirectional test sequentially.
-t, --time n              # Time in seconds to transmit (default 10 secs).
-L, --listenport n        # Port to receive bidirectional tests back on.
-P, --parallel n          # Number of parallel client threads to run.
-S, --tos n               # Set Type of Service (TOS) for outgoing packets.
-T, --ttl n               # Set Time to Live (TTL) for multicast packets.
-F filename               # Use a specific file as the data stream.
```

### Examples

UDP testing is often preferred for measuring link capacity, jitter, and packet loss.

**UDP Mode:**

Server:
```shell
iperf -u -s
```

Client:
```shell
iperf -u -c 192.168.1.1 -b 100M -t 60
```
This tests the upload bandwidth to `192.168.1.1` at a 100Mbps rate for 60 seconds.

**TCP Mode:**

Server:
```shell
iperf -s
```

Client:
```shell
iperf -c 192.168.1.1 -t 60
```
