tracepath
===

Trace the path to a destination host and discover MTU information

## Description

The **tracepath command** is used to trace and display the route that packets take to reach a destination host, while also discovering the Path MTU (Maximum Transmission Unit).

### Syntax

```shell
tracepath [parameters]
```

### Parameters

*   Destination Host: Specifies the destination host to trace;
*   Port: Specifies the UDP port number to use.

### Example

```shell
tracepath www.58.com
 1:  192.168.2.10 (192.168.2.10)                           20.150ms pmtu 1500
 1:  unknown (192.168.2.1)                                  9.343ms
 2:  221.6.45.33 (221.6.45.33)                             34.430ms
 3:  221.6.9.81 (221.6.9.81)                               19.263ms
 4:  122.96.66.37 (122.96.66.37)                           54.372ms
 5:  219.158.96.149 (219.158.96.149)                      asymm  6 128.526ms
 6:  123.126.0.66 (123.126.0.66)                          138.281ms
 7:  124.65.57.26 (124.65.57.26)                          166.244ms
 8:  61.148.154.98 (61.148.154.98)                        103.723ms
 9:  202.106.42.102 (202.106.42.102)                      asymm 10  78.099ms
10:  210.77.139.150 (210.77.139.150)                      asymm  9 199.930ms
11:  211.151.104.6 (211.151.104.6)                        asymm 10 121.965ms
12:  no reply
13:  211.151.111.30 (211.151.111.30)                      asymm 12 118.989ms reached
     Resume: pmtu 1500 hops 13 back 12
```
