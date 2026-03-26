ab
===

A performance testing tool for Apache HTTP server.


## Installation

If not installed, use the following commands:

```shell
# Ubuntu
sudo apt-get install apache2-utils

# CentOS
yum install httpd-tools
```


## Description

The **ab command** is a tool for benchmarking your Apache HTTP server. It allows you to see how your Apache installation performs by providing statistics on the number of requests per second it can handle.

### Syntax

```shell
ab [ -A auth-username:password ] [ -c concurrency ] [ -C cookie-name=value
] [ -d ] [ -e csv-file ] [ -g gnuplot-file ] [ -h ] [ -H custom-header ] [
-i  ]  [  -k  ]  [  -n  requests  ] [ -p POST-file ] [ -P proxy-auth-user‐
name:password ] [ -q ] [ -s ] [ -S ] [ -t timelimit ] [ -T content-type  ]
[  -v verbosity] [ -V ] [ -w ] [ -x <table>-attributes ] [ -X proxy[:port]
]  [  -y  <tr>-attributes  ]  [  -z   <td>-attributes   ]   [http://]host‐
name[:port]/path
```

### Options

```shell
-A auth-username:password
      # Supplies basic authentication credentials to the server. The username 
      # and password are separated by a colon and sent cleartext over the 
      # wire. ab will send them regardless of whether the server requested 
      # them (i.e., it sends an "Authentication: Basic" header).

-c concurrency
      # Number of multiple requests to perform at a time. Default is one 
      # request at a time.

-C cookie-name=value
      # Add a "Cookie:" line to the request. The argument is typically in the 
      # form of a name=value pair. This field is repeatable.

-d    # Do not display the "percentage served within XX [ms] table". 
      # (Legacy support).

-e csv-file
      # Write a Comma Separated Value (CSV) file which contains for each 
      # percentage (from 1% to 100%) the time (in milliseconds) it took to 
      # serve that percentage of the requests. This is usually more useful 
      # than the 'gnuplot' file as the results are already 'binned'.

-g gnuplot-file
      # Write all measured values out as a 'gnuplot' or TSV (Tab Separated 
      # Values) file. This file can easily be imported into packages like 
      # Gnuplot, IDL, Mathematica, Igor, or even Excel. The labels are on 
      # the first line of the file.

-h    # Display usage information.

-H custom-header
      # Append extra headers to the request. The argument is typically in 
      # the form of a valid header line, containing a colon-separated 
      # field-value pair (e.g., 'Accept-Encoding: zip/zop;8 bit').

-i    # Use HTTP HEAD requests instead of GET. Cannot be used with POST.

-k    # Enable the HTTP KeepAlive feature, i.e., perform multiple requests 
      # within one HTTP session. Default is no KeepAlive.

-n requests
      # Number of requests to perform for the benchmarking session. The 
      # default is to just perform a single request, which usually leads 
      # to non-representative benchmarking results.

-p POST-file
      # File containing data to POST. Remember to also set -T.

-P proxy-auth-username:password
      # Supplies basic authentication credentials to a proxy en-route. The 
      # username and password are separated by a colon and sent cleartext 
      # over the wire. ab will send them regardless of whether the proxy 
      # requested them (i.e., it sends a "Proxy-Authorization: Basic" header).

-q    # When processing more than 150 requests, ab outputs a progress count 
      # on stderr every 10% or 100 requests or so. The -q flag will 
      # suppress these messages.

-s    # When compiled in (ab -h will show you), use the SSL protected https 
      # rather than the http protocol. This feature is experimental and 
      # very rudimentary. You probably do not want to use it.

-S    # Do not display the median and standard deviation values, nor 
      # display the warning/error messages when the average and median are 
      # more than one or two times the standard deviation apart. And 
      # default to the min/avg/max values. (Legacy support).

-t timelimit
      # Maximum number of seconds to spend for benchmarking. This 
      # implies a -n 50000 internally. Use this to benchmark the server 
      # within a fixed amount of time. Per default, there is no timelimit.

-T content-type
      # Content-type header to use for POST/PUT data.

-v verbosity
      # Set verbosity level - 4 and above prints information on headers, 
      # 3 and above prints response codes (404, 200, etc.), 2 and above 
      # prints warnings and info.

-V    # Display version number and exit.

-w    # Print results in HTML tables. The default table is two columns 
      # wide, with a white background.

-x <table>-attributes
      # String to use as attributes for <table>. Attributes are inserted 
      # like <table [attributes] >.

-X proxy[:port]
      # Use a proxy server for the requests.

-y <tr>-attributes
      # String to use as attributes for <tr>.

-z <td>-attributes
      # String to use as attributes for <td>.
```

### Parameters

Host: The host to be tested.


### Examples

```shell
# 10 concurrent requests, total of 500 requests
ab -c 10 -n 500 https://www.qq.com/
```
