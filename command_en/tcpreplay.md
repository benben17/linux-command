tcpreplay
===

Replay network traffic captured in pcap files for performance or functional testing

## Description

**tcpreplay** is used to replay network traffic saved in pcap files. It supports replaying traffic at the original capture speed or at a specified rate, limited only by the hardware's capacity.

It allows traffic to be split across two network interfaces, filtered, or edited in various ways, making it an essential tool for testing firewalls, NIDS, and other network devices.

### Parameters

-d number, --dbug=number
Enable debugging output (0-5, default 0). Requires `--enable-debug` configuration.

-q, --quiet
Quiet mode. Only print statistics at the end of the run.

-T string, --timer=string
Select packet timing mode: select, ioport, gtod, nano. Default is `gtod`.
- nano: uses `nanosleep()` API.
- select: uses `select()` API.
- ioport: writes to i386 IO port 0x80.
- gtod: uses `gettimeofday()` loop.

--maxsleep=number
Set the maximum number of milliseconds to sleep between packets (default 0, disabled). Prevents long delays between packets without affecting the majority.

-v, --verbose
Print decoded packets to stdout via `tcpdump`.

-A string, --decode=string
Arguments passed to the `tcpdump` decoder. Must be used with `-v`. Default is `-n -l`. Ensure the string is double-quoted, e.g., `-A "-axxx"`.

-K, --preload-pcap
Preload the pcap file into RAM before sending to improve startup and replay performance. Can be used with or without `--loop`.

-c string, --cachefile=string
Split traffic using a `tcpprep` cache file. Must be used with `intf2`. Cannot be used with `dualfile`. Useful for sending bidirectional traffic through a device.

-2, --dualfile
Replay two files at once from a network tap. Must be used with `intf2`. Cannot be used with `cachefile`. Replays each file on a separate interface, mixing them based on timestamps.

-i string, --intf1=string
Client-to-server/RX/primary traffic output interface.

-I string, --intf2=string
Server-to-client/TX/secondary traffic output interface. Typically used with `--cachefile`.

--listnics
List all available network interfaces and exit.

-l number, --loop=number
Loop through the capture file X times. Use 0 for infinite. Default is 1.

--loopdelay-ms=number
Delay between loops in milliseconds. Default is 0.

--pktlen
Override `snaplen` and use the actual packet length.

-L number, --limit=number
Limit the number of packets to send. Default is -1 (all).

--duration=number
Limit the number of seconds to send traffic. Default is -1 (all).

-x string, --multiplier=string
Modify replay speed by a specified multiple (e.g., 2.0 for double speed, 0.7 for 70%).

-p string, --pps=string
Replay at a fixed packets-per-second rate.

-M string, --mbps=string
Replay at a fixed Mbps rate.

-t, --topspeed
Replay packets as fast as possible.

-o, --oneatatime
Step through packets one at a time based on user input.

--pps-multi=number
Specify the number of packets to send per time interval. Useful for very high rates where sleep precision is difficult.

--unique-ip
Modify IP addresses for each loop iteration to generate unique flows. Must be used with `--loop`.

--unique-ip-loops=string
Number of iterations before assigning new unique IPs. Default is 1.

--netmap
Write packets directly to a netmap-enabled network adapter to achieve line-rate performance. Bypasses the network driver.

--nm-delay=number
Delay in seconds after loading netmap to ensure the interface is fully up. Default is 10.

--no-flow-stats
Suppress printing and tracking of flow statistics.

--flow-expiry=number
Number of inactive seconds before a flow is considered expired (default 0, no expiry). Helps optimize flow timeout settings for network devices.

-P, --pid
Print tcpreplay's PID at startup.

--stats=number
Print statistics every X seconds. If 0, print every loop.

-V, --version
Print version information.

-h, --less-help
Print simple help information.

-H, --help
Print full help information.

### Examples

**1. Replay captured FTP traffic**
a. Capture FTP traffic using a sniffer and save as `ftp.pcap`.
b. Create a cache file using `tcpprep`:
   `tcpprep -an client -i ftp.pcap -o ftp.cache -v`
c. Replay the traffic through a DUT (Device Under Test):
   `tcpreplay -c ftp.cache -i eth0 -j eth1 ftp.pcap -R -v`
   `-R` sends at full speed, `-v` shows verbose output.

**2. Replay BT (BitTorrent) traffic**
a. Capture BT traffic and save as `bt.pcap`.
b. Create a cache file:
   `tcpprep -an client -i bt.pcap -o bt.cache -C "100M BT Packet" -v`
c. Replay:
   `tcpreplay -c bt.cache -i eth0 -j eth1 bt.pcap -v -R`

**3. Replay TFTP traffic**
a. Capture TFTP traffic and save as `tftp.pcap`.
b. Create a cache file:
   `tcpprep -an server -i tftp.pcap -o tftp.cache -v`
c. Replay:
   `tcpreplay -c tftp.cache -i eth0 -j eth1 tftp.pcap -v`

**4. Replay pcap with specific rate and loops**
   `tcpreplay -i eth1 -M 10 -l 0 /home/demo/LSDK/LSDK.pcap`
   Replays at 10Mbps in an infinite loop.
吐
