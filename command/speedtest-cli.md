speedtest-cli
===

Test internet speed from the command line.

## Description

**speedtest-cli** is a command-line interface for testing internet bandwidth using speedtest.net. It is written in Python and allows you to test both download and upload speeds. Project URL: https://github.com/sivel/speedtest-cli

### Installation

`speedtest-cli` requires Python 2.4-3.4 (or later). Choose the installation method that suits you best.

**Using pip:**

```shell
# pip install speedtest-cli
```

**Using easy_install:**

```shell
# easy_install speedtest-cli
```

**Using github + pip:**

```shell
# pip install git+https://github.com/sivel/speedtest-cli.git
```

Or:

```shell
# git clone https://github.com/sivel/speedtest-cli.git
# python speedtest-cli/setup.py install
```

**Downloading the script directly:**

```shell
# wget -O speedtest-cli https://raw.github.com/sivel/speedtest-cli/master/speedtest_cli.py
# chmod +x speedtest-cli
```

Or:

```shell
# curl -o speedtest-cli https://raw.github.com/sivel/speedtest-cli/master/speedtest_cli.py
# chmod +x speedtest-cli
```

After downloading the script, just give it execution permissions.

### Usage

```shell
-h, --help       Show this help message and exit
--share          Generate and provide a URL to the speedtest.net share results image
--simple         Suppress verbose output, only show basic information
--list           Display a list of speedtest.net servers sorted by distance
--server=SERVER  Specify a server ID from the list to test against
--mini=MINI      URL of the Speedtest Mini server
--source=SOURCE  Source IP address to bind to
--version        Show the version number and exit
```

### Examples

List all test servers in China:

```shell
[root@li229-122 ~]# speedtest-cli --list | grep China
1185) China Unicom (Changchun, China) [10534.35 km]
3784) China Mobile (Urumqi, China) [10581.15 km]
2667) Beijing Normal University (Beijing, China) [11117.03 km]
2529) Beijing Normal University (Beijing, China) [11117.03 km]
2816) Capital Online Data service (Beijing, China) [11117.03 km]
4354) SXmobile (Taiyuan, China) [11383.17 km]
3973) China Telecom (Lanzhou, China) [11615.43 km]
3633) China Telecom (Shanghai, China) [11983.37 km]
3927) China Mobile Jiangsu Co., Ltd. (Suzhou, China) [11989.27 km]
2461) China Unicom (Chengdu, China) [12213.35 km]
1028) Shepherd Software (Xiamen, China) [12785.57 km]
1628) Xiamen Guangdian Xinxu (Xiamen, China) [12785.57 km]
3891) GZinternet (Guangzhou, China) [13005.36 km]
3871) SZWCDMA (Shenzhen, China) [13059.20 km]
3819) SZU (Shenzhen, China) [13059.20 km]
1536) STC (Hong Kong, China) [13088.37 km]
1890) Telin (Hong Kong, China) [13088.37 km]
```

**Interpreting the Results:**

```shell
3633) China Telecom (Shanghai, China) [11983.37 km]
```

* `3633`: Server ID
* `China Telecom`: ISP (Internet Service Provider)
* `Shanghai, China`: Server location
* `11983.37 km`: Geographic distance between your machine and the server.

**Performing a Speed Test:**

```shell
[root@li229-122 ~]# speedtest-cli --server=3633 --share
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Testing from Linode (173.255.219.122)...
Hosted by China Telecom (Shanghai) [11983.37 km]: 23.603 ms
Testing download speed........................................
Download: 24.84 Mbit/s
Testing upload speed..................................................
Upload: 4.57 Mbit/s
Share results: http://www.speedtest.net/result/3240988007.png
```
