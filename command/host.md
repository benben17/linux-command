host
===

A utility for performing DNS lookups.

## Supplemental Information

The **host command** is a commonly used utility for analyzing DNS. It can be used to test if the Domain Name System is working correctly.

### Syntax

```shell
host (options) (parameters)
```

### Options

```shell
-a: Display all DNS information (equivalent to -v -t ANY);
-c <class>: Specify the query class (default is "IN");
-C: Query for the complete SOA record for the zone;
-r: Disable recursive lookup;
-t <type>: Specify the query type (e.g., A, MX, NS, CNAME, etc.);
-v: Display verbose output;
-w: Wait forever for a response from the server;
-W <timeout>: Wait up to <timeout> seconds for a response;
-4: Use IPv4 only;
-6: Use IPv6 only.
```

### Parameters

Host: The hostname or IP address to query.

### Examples

```shell
[root@localhost ~]# host www.jsdig.com 
www.jsdig.com is an alias for host.1.jsdig.com.
host.1.jsdig.com has address 100.42.212.8

[root@localhost ~]# host -a www.jsdig.com
Trying "www.jsdig.com"
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34671
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.jsdig.com.               IN      ANY

;; ANSWER SECTION:
www.jsdig.com.        463     IN      CNAME   host.1.jsdig.com.

Received 54 bytes from 202.96.104.15#53 in 0 ms
```
