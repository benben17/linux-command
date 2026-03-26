ngrep
===

Network packet matching and display tool

## Description

The **ngrep command** is the network version of `grep`. It strives to provide many of `grep`'s features for searching network packets. Since `ngrep` relies on the `libpcap` library, it supports a wide range of operating systems and network protocols. It can identify TCP, UDP, and ICMP packets and understands BPF (Berkeley Packet Filter) filtering mechanisms.

### Installation

The project homepage is http://ngrep.sourceforge.net/. It requires `libpcap` (http://www.tcpdump.org/). You can typically install `libpcap` using your package manager (e.g., `yum install libpcap`).

If you need to install `libpcap` from source:

```shell
wget http://www.tcpdump.org/release/libpcap-1.3.0.tar.gz
tar -zxf libpcap-1.3.0.tar.gz
cd libpcap-1.3.0
./configure
make && make install
```

Then install `ngrep` using the standard `configure`, `make`, and `make install` steps.

Note: If you encounter the "please wipe out all unused pcap installations" error during configuration, use the following option:

```shell
./configure --with-pcap-includes=/usr/local/include/pcap
```

Verify the installation by typing `ngrep` in the terminal.

### Syntax

```shell
ngrep <-LhNXViwqpevxlDtTRM> <-IO pcap_dump> <-n num> <-d dev> <-A num>
<-s snaplen> <-S limitlen> <-w normal|byline|single|none> <-c cols>
<-P char> <-F file> <match expression> <bpf filter>
```

### Options

```shell
-e: Display empty packets.
-i: Ignore case.
-v: Invert match.
-R: Don't do privilege revocation logic.
-x: Display in hexadecimal format.
-X: Match in hexadecimal format.
-w: Match as whole words.
-p: Do not use promiscuous mode.
-l: Make stdout line buffered.
-D: Replay pcap_dumps with their recorded time intervals.
-t: Display a timestamp before each matching packet.
-T: Display the time interval between matching packets.
-M: Perform single-line matching only.
-I: Read data from a pcap file.
-O: Save matching data to a pcap file.
-n: Capture and display only the specified number of packets.
-A: Dump the specified number of packets after a match.
-s: Set the BPF caplen (snapshot length).
-S: Set the limit length on matched packets.
-W: Set the display format (e.g., "byline" to respect newlines in packets).
-c: Force column width.
-P: Set the non-printable display character.
-F: Read BPF filter from a file.
-N: Show sub-protocol numbers defined by IANA.
-d: Specify the network interface to use (use -L to list available interfaces).
-L: List available network interfaces.
```

### Examples

Capture requests and responses on port 18080. `-W byline` is used to parse newlines in the packets for better readability. `-d lo` listens on the loopback interface:

```shell
ngrep -W byline -d lo port 18080
```

Capture traffic on port 80. `-d eth0` specifies the external interface:

```shell
ngrep -W byline -d eth0 port 80
```

Capture all packets containing letters on port 18080:

```shell
ngrep '[a-zA-Z]' -t -W byline -d any tcp port 18080
```

Capture the string `.flv`. For example, to find the download URL of a `.flv` video file:

```shell
ngrep -d3 -N -q \.flv
interface: \Device\TNT_40_1_{670F6B50-0A13-4BAB-9D9E-994A833F5BA9} (10.132.0.0/2
55.255.192.0)
match: \.flv
```

After opening a video page:

```shell
T(6) 10.132.34.23:24860 -> 61.142.208.154:80 [AP]
GET /f59.c31.56.com/flvdownload/12/19/ggyg7741@56.com_56flv_zhajm_119556973
97.flv HTTP/1.1..accept: */*..Referer: http://www.56.com/flashApp/v_player_
site.swf..x-flash-version: 9,0,45,0..UA-CPU: x86..Accept-Encoding: gzip, de
flate..User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; .NET
CLR 2.0.50727; .NET CLR 3.0.04506.30)..host: f59.r.56.com..Connection: Keep
-Alive..Cookie: whistoryview=23423759-23635627-23423344-23171935-23058374-2
3081156-23207350-22395727-; geoip=............; wl_all_s=y....
```

The URL is found: http://f59.c31.56.com/flvdownload/12/19/ggyg7741@56.com_56flv_zhajm_11955697397.flv

Adding the `-W byline` parameter makes the output much more readable:

```shell
T(6) 2007/11/25 15:56:12.192619 10.132.34.23:26365 -> 59.151.21.101:80 [AP]
GET /aa.flv HTTP/1.1.
Accept: */*.
Accept-Language: zh-cn.
UA-CPU: x86.
Accept-Encoding: gzip, deflate.
User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; .NET CLR 2.0.5072
7; .NET CLR 3.0.04506.30).
Host: www.google.cn.
Connection: Keep-Alive.
Cookie: PREF=id=a0b2932c336477e9:TB=4:NW=1:TM=1187877372:LM=1187956074:S=Y1Fzndp
rT3vFo7ac; SID=DQAAAHcAAABJCEXeOVLHu2rIfb5BfKP3GG9PbhJDEkXsLTV8y0f_lvSd2Y46Q0FPt
83CnEs9rxA1xBDM9mLR8-ckWeScyOQA8PyYnX5u5OjFvjfRbDg_FDZfwxhRzqS9KPZv26pjnsUxs0FDM
1xpJ5AgDn38pXtlCdkksJ0-cbiIWoA61oHWMg; NID=7=AvJxn5B6YOLLxoYz4LLzhIbNsQUQiulRS6U
JGxdBniQBmXm99y7L-NBNORN82N3unmZSGHFPfePVHnLK2MjYjglyXZhU9x7ETXNBnY3NurNijHDhJ7K
yi7E53UBOcv4V.
```
