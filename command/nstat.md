nstat
===

nstat is a simple tool for monitoring kernel SNMP counters and network interface statistics.

## Description

Most command-line users are familiar with `netstat`, which is part of the `net-tools` package. In modern Linux distributions, `net-tools` is largely deprecated and replaced by the `iproute2` suite, to which `nstat` belongs.

### Syntax

```shell
nstat [OPTION] [ PATTERN [ PATTERN ] ]
```

### Options

```shell
-h: Display help message.
-V: Display version information.
-z: Dump zero counters. By default, counters with a value of zero are not shown.
-r: Reset history statistics (clear history).
-n: Do not display anything, only update the history.
-a: Display absolute values of counters.
-d: Run in daemon mode and collect statistics.
-s: Do not update history.
-j: Output in JSON format.
```

### Examples

Run `nstat` to query the status of network interfaces. The following shows statistics for IPv4, IPv6, TCP, UDP, and ICMP:

```shell
nstat          
#kernel
IpInReceives                    769152             0.0
IpInAddrErrors                  1                  0.0
IpInDelivers                    769146             0.0
IpOutRequests                   764236             0.0
IpOutDiscards                   20                 0.0
IpOutNoRoutes                   1                  0.0
IcmpInMsgs                      92                 0.0
IcmpInDestUnreachs              92                 0.0
IcmpOutMsgs                     94                 0.0
IcmpOutDestUnreachs             94                 0.0
IcmpMsgInType3                  92                 0.0
IcmpMsgOutType3                 94                 0.0
TcpActiveOpens                  1786               0.0
TcpPassiveOpens                 142                0.0
TcpAttemptFails                 11                 0.0
TcpEstabResets                  72                 0.0
TcpInSegs                       756827             0.0
TcpOutSegs                      802908             0.0
TcpRetransSegs                  767                0.0
TcpOutRsts                      702                0.0
UdpInDatagrams                  12075              0.0
UdpNoPorts                      82                 0.0
UdpOutDatagrams                 7045               0.0
UdpIgnoredMulti                 70                 0.0
Ip6InReceives                   5005               0.0
Ip6InDelivers                   5005               0.0
Ip6OutRequests                  131                0.0
Ip6OutDiscards                  2                  0.0
Ip6OutNoRoutes                  959                0.0
Ip6InMcastPkts                  4999               0.0
Ip6OutMcastPkts                 125                0.0
Ip6InOctets                     797462             0.0
Ip6OutOctets                    16421              0.0
Ip6InMcastOctets                797030             0.0
Ip6OutMcastOctets               15949              0.0
Ip6InNoECTPkts                  5005               0.0
Icmp6InMsgs                     3                  0.0
Icmp6OutMsgs                    51                 0.0
Icmp6InNeighborAdvertisements   1                  0.0
Icmp6InMLDv2Reports             2                  0.0
Icmp6OutRouterSolicits          11                 0.0
Icmp6OutNeighborSolicits        4                  0.0
Icmp6OutMLDv2Reports            36                 0.0
Icmp6InType136                  1                  0.0
Icmp6InType143                  2                  0.0
Icmp6OutType133                 11                 0.0
Icmp6OutType135                 4                  0.0
Icmp6OutType143                 36                 0.0
Udp6InDatagrams                 4998               0.0
Udp6OutDatagrams                76                 0.0
TcpExtTW                        385                0.0
TcpExtPAWSEstab                 1                  0.0
TcpExtDelayedACKs               37133              0.0
TcpExtDelayedACKLocked          57                 0.0
TcpExtDelayedACKLost            456                0.0
TcpExtTCPHPHits                 417717             0.0
TcpExtTCPPureAcks               34186              0.0
TcpExtTCPHPAcks                 222980             0.0
TcpExtTCPSACKReorder            1                  0.0
TcpExtTCPLossUndo               194                0.0
TcpExtTCPLostRetransmit         169                0.0
TcpExtTCPSlowStartRetrans       1                  0.0
TcpExtTCPTimeouts               494                0.0
TcpExtTCPLossProbes             309                0.0
TcpExtTCPBacklogCoalesce        571                0.0
TcpExtTCPDSACKOldSent           281                0.0
TcpExtTCPDSACKRecv              281                0.0
TcpExtTCPAbortOnData            13                 0.0
TcpExtTCPAbortOnClose           30                 0.0
TcpExtTCPDSACKIgnoredOld        1                  0.0
TcpExtTCPDSACKIgnoredNoUndo     258                0.0
TcpExtTCPSackShiftFallback      1                  0.0
TcpExtTCPRcvCoalesce            18314              0.0
TcpExtTCPFastOpenActiveFail     2                  0.0
TcpExtTCPSpuriousRtxHostQueues  11                 0.0
TcpExtTCPAutoCorking            1684               0.0
TcpExtTCPFromZeroWindowAdv      2                  0.0
TcpExtTCPToZeroWindowAdv        2                  0.0
TcpExtTCPSynRetrans             479                0.0
TcpExtTCPOrigDataSent           359814             0.0
TcpExtTCPHystartTrainDetect     13                 0.0
TcpExtTCPHystartTrainCwnd       550                0.0
TcpExtTCPKeepAlive              18                 0.0
TcpExtTCPDelivered              361695             0.0
TcpExtTCPZeroWindowDrop         1                  0.0
TcpExtTcpTimeoutRehash          494                0.0
TcpExtTcpDuplicateDataRehash    2                  0.0
TcpExtTCPDSACKRecvSegs          281                0.0
IpExtInNoRoutes                 3                  0.0
IpExtInMcastPkts                5392               0.0
IpExtOutMcastPkts               221                0.0
IpExtInBcastPkts                70                 0.0
IpExtOutBcastPkts               10                 0.0
IpExtInOctets                   2100280442         0.0
IpExtOutOctets                  226760631          0.0
IpExtInMcastOctets              746608             0.0
IpExtOutMcastOctets             27565              0.0
IpExtInBcastOctets              5674               0.0
IpExtOutBcastOctets             778                0.0
IpExtInNoECTPkts                1885871            0.0
```
