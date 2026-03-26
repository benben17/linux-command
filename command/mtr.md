mtr
===

Network diagnostic tool that combines the functionality of `traceroute` and `ping`

## Description

**mtr** is used to investigate the network connection between the host it is running on and a user-specified destination host. After determining the address of each network hop between machines, it sends a series of ICMP ECHO requests to each machine to determine the quality of the link. During this process, it prints performance statistics for each hop.

The `mtr` command is often built-in on Debian-based distributions and can be installed on other distributions. it supports most major operating systems.
For more details, visit the [official website](https://www.bitwizard.nl/mtr).

### Syntax

```shell
mtr [options] [target_ip/domain]
```

### Parameters

| Parameter | Description |
| --------- | ----------- |
| `-r`      | Report mode: displays a report after the specified number of cycles. |
| `-c`      | Number of pings to send to each hop (default is 10). |
| `-n`      | No DNS resolution: displays IP addresses instead of hostnames. |
| `-s`      | Specify the size of the ping packets. |
| `--report`| Same as `-r`, output results in report mode instead of interactive display. |

### Examples

Use the `-r` parameter to display a report:

```shell
[root@localhost ~]# mtr -r github.com

HOST: WIKIHOST                    Loss%   Snt   Last   Avg  Best  Wrst  StDev
  1.|-- 161.129.42.1               0.0%    10    0.5   0.5   0.4   0.6   0.1
  2.|-- 10.12.52.0                 0.0%    10    0.9   1.2   0.8   3.4   0.8
  3.|-- unn-138-199-1-182.cdn77.c  0.0%    10    0.9   0.8   0.8   0.9   0.1
  4.|-- 63.217.254.209            70.0%    10    1.3   1.3   1.2   1.3   0.0
  5.|-- 63-216-176-146.static.pcc  0.0%    10    4.1   3.6   1.1  12.9   3.5
  6.|-- ae27-0.icr02.hkg20.ntwk.m  0.0%    10    2.8   5.5   1.7  24.0   6.9
  7.|-- be-102-0.ibr01.hkg20.ntwk 20.0%    10   36.4  36.5  36.3  36.7   0.1
  8.|-- be-10-0.ibr01.sg3.ntwk.ms 50.0%    10   36.4  37.3  36.3  39.5   1.4
  9.|-- ae100-0.icr01.sg3.ntwk.ms  0.0%    10   35.9  38.8  35.9  53.3   5.4
 10.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
 11.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
 12.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
 13.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
 14.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
 15.|-- 20.205.243.166             0.0%    10   35.7  35.8  35.7  35.9   0.0
```

Use the `-c` parameter to set the number of packets sent:

```shell
[root@localhost ~]# mtr -r -c 30 github.com

HOST: WIKIHOST                    Loss%   Snt   Last   Avg  Best  Wrst  StDev
  1.|-- 161.129.42.1               0.0%    30    0.5   0.4   0.3   1.2   0.2
  2.|-- 10.12.52.0                 0.0%    30    0.8   1.2   0.8   9.2   1.6
  3.|-- unn-138-199-1-182.cdn77.c  0.0%    30    0.9   0.9   0.8   3.0   0.4
  4.|-- 63.217.254.209            40.0%    30    1.3   1.3   1.1   2.4   0.3
  5.|-- 63-216-176-146.static.pcc  0.0%    30    3.0   3.1   1.0  13.5   3.4
  6.|-- ae27-0.icr02.hkg20.ntwk.m  0.0%    30    1.7   2.2   1.6   5.7   0.9
  7.|-- be-102-0.ibr01.hkg20.ntwk  6.7%    30   36.4  36.6  36.3  38.9   0.5
  8.|-- be-10-0.ibr01.sg3.ntwk.ms 50.0%    30   36.7  47.1  36.2 102.7  21.0
  9.|-- ae100-0.icr01.sg3.ntwk.ms  0.0%    30   36.1  41.4  35.9  78.4   8.8
 10.|-- ???                       100.0    30    0.0   0.0   0.0   0.0   0.0
 11.|-- ???                       100.0    30    0.0   0.0   0.0   0.0   0.0
 12.|-- ???                       100.0    30    0.0   0.0   0.0   0.0   0.0
 13.|-- ???                       100.0    30    0.0   0.0   0.0   0.0   0.0
 14.|-- ???                       100.0    30    0.0   0.0   0.0   0.0   0.0
 15.|-- 20.205.243.166             0.0%    30   35.7  35.8  35.6  35.8   0.0
```

Use the `-s` parameter to specify the size of `ping` packets:

```shell
[root@localhost ~]# mtr -r -c 30 -s 1024 github.com

HOST: WIKIHOST                    Loss%   Snt   Last   Avg  Best  Wrst  StDev
  1.|-- 161.129.42.1               0.0%    30    0.6   0.6   0.3   4.3   0.7
  2.|-- 10.12.52.0                 0.0%    30    1.0   1.1   0.8   7.0   1.1
  3.|-- unn-138-199-1-182.cdn77.c  0.0%    30    0.9   0.9   0.8   1.1   0.1
  4.|-- 63.217.254.209            66.7%    30    1.3   1.3   1.2   1.5   0.1
  5.|-- 63-216-176-146.static.pcc  0.0%    30    3.1   3.3   1.0  18.4   4.5
  6.|-- ae27-0.icr02.hkg20.ntwk.m  0.0%    30    2.2   3.7   1.7  12.2   2.5
  7.|-- be-102-0.ibr01.hkg20.ntwk  6.7%    30   36.5  36.6  36.4  38.9   0.5
  8.|-- be-10-0.ibr01.sg3.ntwk.ms 33.3%    30   38.3  36.9  36.3  39.1   0.7
  9.|-- ae100-0.icr01.sg3.ntwk.ms  0.0%    30   36.1  38.4  35.9  66.6   5.9
 10.|-- ???                       100.0    30    0.0   0.0   0.0   0.0   0.0
```
