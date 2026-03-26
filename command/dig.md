dig
===

Domain Information Groper.

## Description

The **dig** command is a flexible tool for interrogating DNS name servers. It can be used to test if the Domain Name System is working correctly.

### Syntax

```shell
dig (options) (parameters)
```

### Options

```shell
@<server_address>   Specify the name server to query.
-b <ip_address>     Specify which local IP address to use when the host has multiple IP addresses.
-f <filename>       Batch mode: read a list of query tasks from the specified file.
-p <port>           Specify the port number of the name server.
-t <type>           Specify the resource record type to query.
-x <ip_address>     Reverse lookup (IP to name).
-4                  Use IPv4 only.
-6                  Use IPv6 only.
-h                  Display help information.
```

### Parameters

* Host: The domain name or host to query.
* Query Type: The type of DNS record (e.g., A, MX, NS).
* Query Class: The class of DNS record (e.g., IN).
* Query Options: Additional query options.

### Examples

```shell
[root@localhost ~]# dig www.baidu.com

; <<>> DiG 9.10.6 <<>> www.baidu.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 57295
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;www.baidu.com.			IN	A

;; ANSWER SECTION:
www.baidu.com.		963	IN	CNAME	www.a.shifen.com.
www.a.shifen.com.	63	IN	A	180.101.50.242
www.a.shifen.com.	63	IN	A	180.101.50.188

;; Query time: 14 msec
;; SERVER: 119.29.29.29#53(119.29.29.29)
;; WHEN: Wed May 10 16:16:36 CST 2023
;; MSG SIZE  rcvd: 101
```
