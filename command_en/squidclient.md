squidclient
===

Client management tool for Squid servers.

## Description

The **squidclient command** is a command-line tool for managing Squid servers. It can be used to view detailed running information and perform administrative tasks on a Squid server.

### Syntax

```shell
squidclient [option] [parameter]
```

### Options

```shell
-a: Do not include an "Accept:" header;
-r: Force a cache reload of the URL;
-s: Quiet mode, do not output information to standard output (stdout);
-h: Retrieve the URL from the specified host;
-l: Specify a local IP address to bind to;
-p: Port number, defaults to 3128;
-m: Specify the HTTP method to send (e.g., GET, POST, PURGE);
-u: Username for proxy authentication.
```

### Parameter

URL: Specify the URL in the cache to operate on.
