curl
===

A command-line tool for transferring data using URL syntax

## Supplemental Information

The **curl command** is a tool for transferring data from or to a server using one of the supported protocols (HTTP, HTTPS, FTP, FTPS, SCP, SFTP, TFTP, DICT, TELNET, LDAP, or FILE). The command is designed to work without user interaction. curl offers a wide range of features such as proxy support, user authentication, FTP upload, HTTP post, SSL connections, cookies, file transfer resume, and more. It is an excellent tool for automating web-related tasks and data retrieval.

### Syntax

```shell
curl (options) (parameters)
```

### Options

```bash
-a   --append                                   # Append to target file when uploading
-A   --user-agent                               # Send user-agent string to server
-anyauth                                        # Use "any" authentication method
-b   --cookie                                   # Cookie string or file to read from
     --basic                                    # Use HTTP Basic Authentication
-B   --use-ascii                                # Use ASCII/text transfer
-c   --cookie-jar                               # Write cookies to this file after operation
-C   --continue-at                              # Resume transfer from a specific offset
-d   --data                                     # Send data in an HTTP POST request
     --data-ascii                               # Post data as ASCII
     --data-binary                              # Post data as binary
     --negotiate                                # Use HTTP Negotiate (SPNEGO) authentication
     --digest                                   # Use HTTP Digest authentication
     --disable-eprt                             # Disable EPRT or LPRT
     --disable-epsv                             # Disable EPSV
-D   --dump-header                              # Write protocol headers to file
     --egd-file                                 # Set EGD socket path for random data (SSL)
     --tcp-nodelay                              # Use TCP_NODELAY option
-e   --referer                                  # Referrer URL
-E   --cert                                     # Client certificate file and password (SSL)
     --cert-type                                # Certificate file type (DER/PEM/ENG) (SSL)
     --key                                      # Private key file name (SSL)
     --key-type                                 # Private key file type (DER/PEM/ENG) (SSL)
     --pass                                     # Passphrase for the private key (SSL)
     --engine                                   # Crypto engine to use (SSL). Use "--engine list" for list
     --cacert                                   # CA certificate to verify peer against (SSL)
     --capath                                   # CA directory to verify peer against (SSL)
     --ciphers                                  # SSL ciphers to use
     --compressed                               # Request compressed response (using deflate or gzip)
     --connect-timeout                          # Maximum time allowed for connection
     --create-dirs                              # Create local directory hierarchy
     --crlf                                     # Convert LF to CRLF when uploading
-f   --fail                                     # Fail silently (no output) on HTTP errors
     --ftp-create-dirs                          # Create remote directories if they don't exist
     --ftp-method [multicwd/nocwd/singlecwd]   # Control CWD usage
     --ftp-pasv                                 # Use PASV/EPSV instead of PORT
     --ftp-skip-pasv-ip                         # Skip the IP address for PASV
     --ftp-ssl                                  # Try SSL/TLS for FTP transfer
     --ftp-ssl-reqd                             # Require SSL/TLS for FTP transfer
-F   --form                                     # Emulate HTTP form post data
     --form-string                              # Emulate HTTP form post data
-g   --globoff                                  # Disable URL sequences and ranges using {} and []
-G   --get                                      # Send data using HTTP GET
-H   --header                                   # Pass custom header to server
     --ignore-content-length                    # Ignore the Content-Length header
-i   --include                                  # Include protocol headers in the output
-I   --head                                     # Show document info (headers) only
-j   --junk-session-cookies                     # Ignore session cookies when reading from file
     --interface                                # Use specified network interface/address
     --krb4                                     # Use krb4 with specified security level
-k   --insecure                                 # Allow insecure connections (SSL)
-K   --config                                   # Read config from file
-l   --list-only                                # List only names of an FTP directory
     --limit-rate                               # Limit transfer speed
     --local-port                               # Force use of a specific local port number
-m   --max-time                                 # Maximum time allowed for the entire operation
     --max-redirs                               # Maximum number of redirects to follow
     --max-filesize                             # Maximum file size to download
-M   --manual                                   # Display full manual
-n   --netrc                                    # Read username and password from .netrc file
     --netrc-optional                           # Use .netrc or URL to override -n
     --ntlm                                     # Use HTTP NTLM authentication
-N   --no-buffer                                # Disable output buffering
-o   --output                                   # Write output to file
-O   --remote-name                              # Write output to file named like the remote file
-p   --proxytunnel                              # Operate through an HTTP proxy tunnel
     --proxy-anyauth                            # Use any proxy authentication method
     --proxy-basic                              # Use Basic authentication on the proxy
     --proxy-digest                             # Use Digest authentication on the proxy
     --proxy-ntlm                               # Use NTLM authentication on the proxy
-P   --ftp-port                                 # Use port address instead of PASV
-q                                              # Disable reading .curlrc (must be first argument)
-Q   --quote                                    # Send arbitrary command to FTP server before transfer
-r   --range                                    # Retrieve a byte range from HTTP/1.1 or FTP server
--range-file                                    # Read random file (SSL)
-R   --remote-time                              # Set the remote file's time on the local output
     --retry                                    # Number of retries on transient errors
     --retry-delay                              # Wait time between retries
     --retry-max-time                           # Maximum time to keep retrying
-s   --silent                                   # Silent mode. Don't show progress meter or error messages
-S   --show-error                               # Show error messages even in silent mode
     --socks4                                   # Use SOCKS4 proxy on given host and port
     --socks5                                   # Use SOCKS5 proxy on given host and port
     --stderr                                   # Redirect stderr to specified file
-t   --telnet-option                            # Set telnet option
     --trace                                    # Enable full trace dump of all data to file
     --trace-ascii                              # Enable full trace dump but without hex output
     --trace-time                               # Add timestamp to trace/verbose output
-T   --upload-file                              # Transfer local file to remote
     --url <url>                                # URL to work with
-u   --user                                     # Server user and password
-U   --proxy-user                               # Proxy user and password
-w   --write-out [format]                      # Output specified format after completion
-x   --proxy                                    # Use proxy on given port
-X   --request                                  # Specify request command to use
-y   --speed-time                               # Time to wait before abandoning low speed limit (default 30)
-Y   --speed-limit                              # Stop transfer if speed is lower than this for speed-time
```

### Examples

#### **Downloading Files**

The curl command can be used to perform downloads, send various HTTP requests, specify HTTP headers, etc. curl outputs the downloaded file to stdout and progress information to stderr. Use the `--silent` option to hide progress information.

```shell
curl URL --silent
```

This command outputs the downloaded file to the terminal, writing all data to stdout.

Use the `-O` option to write the downloaded data to a file with the same name as the remote file:

```shell
curl http://example.com/text.iso --silent -O
```

The `-o` option writes the downloaded data to a file with a specified name, and `--progress` displays a progress bar:

```shell
curl http://example.com/test.iso -o filename.iso --progress
######################################### 100.0%
```

#### **Suppressing Errors and Progress Information**

The `-s` parameter suppresses error and progress information.

```shell
curl -s https://www.example.com
# If an error occurs, no error message will be displayed. If no error occurs, results will be shown normally.
```

To prevent curl from producing any output, use the following command:

```shell
curl -s -o /dev/null https://example.com
```

#### **Resuming Downloads**

curl can resume a download from a specific file offset:

```shell
curl URL/File -C offset

# Offset is an integer in bytes. To let curl automatically determine the correct resume position, use -C -:
curl -C - URL
```

#### **Setting the Referrer String**

The Referer header is a string in the HTTP header that indicates which page the user came from.

Use the `--referer` option to specify the referrer string:

```shell
curl --referer http://www.example.com http://example.com
```

#### **Setting the User-Agent String**

Some websites may require a specific browser. You can set the User-Agent string to emulate a browser like IE. Use the `--user-agent` or `-A` option:

```shell
curl URL --user-agent "Mozilla/5.0"
curl URL -A "Mozilla/5.0"
```

Other HTTP headers can also be sent using curl with the `-H` option. For example:

```shell
curl -H "Host:example.com" -H "accept-language:zh-cn" URL
```

#### **Bandwidth Control and Download Quota**

Use `--limit-rate` to restrict the download speed:

```shell
curl URL --limit-rate 50k
```

Specify the limit with k (kilobytes) or m (megabytes).

Use `--max-filesize` to specify the maximum file size that can be downloaded:

```shell
curl URL --max-filesize bytes
```

If the file size exceeds the limit, the command returns a non-zero exit code.

```shell
curl --limit-rate 200k https://example.com
# This command limits the bandwidth to 200 KB/s.
```

#### **Authentication with curl**

Use the `-u` option for HTTP or FTP authentication:

```shell
curl -u user:pwd http://example.com
curl -u user http://example.com
```

#### **Printing Response Headers Only**

Use `-I` or `--head` to print only the HTTP headers:

```shell
[root@localhost text]# curl -I http://example.com
HTTP/1.1 200 OK
Content-Encoding: gzip
Accept-Ranges: bytes
Age: 275552
Cache-Control: max-age=604800
Content-Type: text/html; charset=UTF-8
Date: Mon, 24 Apr 2023 14:39:36 GMT
Etag: "3147526947+gzip"
Expires: Mon, 01 May 2023 14:39:36 GMT
Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
Server: ECS (sec/96EE)
X-Cache: HIT
Content-Length: 648
```

#### **GET Request**

```shell
curl "http://www.example.com"    # If the URL points to a file or image, it will be downloaded.
curl -i "http://www.example.com" # Display all information including headers.
curl -l "http://www.example.com" # List only (for FTP).
curl -v "http://www.example.com" # Display full process of the GET request.
```

#### **POST Request**

```shell
$ curl -d "param1=value1&param2=value2" "http://www.example.com/login"

$ curl -d 'login=emma&password=123' -X POST https://example.com/login
# Or
$ curl -d 'login=emma' -d 'password=123' -X POST https://example.com/login
```

The `--data-urlencode` parameter is similar to `-d` but automatically URL-encodes the data.

```shell
curl --data-urlencode 'comment=hello world' https://example.com/login
```

#### **Sending Text from a Local File**

```shell
curl -d '@data.txt' https://example.com/upload
# Reads the content of data.txt and sends it as the data body.
```

#### **JSON POST Request**

```shell
curl -l -H "Content-type: application/json" -X POST -d '{"phone":"13888888888","password":"test"}' http://example.com/apis/users.json
```

#### **Sending Cookies**

Use `--cookie "COOKIES"` to specify cookies (separate multiple cookies with semicolons):

```shell
curl http://example.com --cookie "user=root;pass=123456"
```

Save cookies to a file using `--cookie-jar`:

```shell
curl URL --cookie-jar cookie_file
```

The `-b` parameter is used to send cookies to the server.

```shell
curl -b 'foo=bar' https://example.com
```

#### **Writing Cookies to a File**

```shell
curl -c cookies.txt https://www.example.com
```

#### **Setting the Referer Header**

The `-e` parameter sets the `Referer` header.

```shell
curl -e 'https://example.com?q=example' https://www.example.com
```

You can also use `-H` to set the `Referer` header.

```shell
curl -H 'Referer: https://example.com?q=example' https://www.example.com
```

#### **Uploading Binary Files**

Use `-F` to upload binary files.

```shell
curl -F 'file=@photo.png' https://example.com/profile
# This adds the header Content-Type: multipart/form-data and uploads photo.png.
```

Specify the MIME type with `-F`:

```shell
curl -F 'file=@photo.png;type=image/png' https://example.com/profile
```

Specify the filename:

```shell
curl -F 'file=@photo.png;filename=me.png' https://example.com/profile
```

#### **Setting Request Headers**

The `-H` parameter adds HTTP request headers.

```shell
curl -H 'Accept-Language: en-US' https://example.com
```

#### **Skipping SSL Verification**

```shell
curl -k https://www.example.com
# This skips the SSL certificate check.
```

#### **Following Redirects**

The `-L` parameter tells curl to follow HTTP redirects.

```shell
curl -L -d 'tweet=hi' https://api.example.com/tweet
```

Note: This does not follow HTML meta refreshes.

#### **Debugging**

The `-v` parameter outputs the entire communication process for debugging.

```shell
curl -v https://www.example.com
# The --trace parameter can also be used for debugging and outputs raw binary data.
```

```shell
curl --trace - https://www.example.com
```

#### **Get Public IP Address**

```shell
curl ipecho.net/plain
```

#### **Testing Website Load Speed**

Use the `-w` option to print statistics after the request is completed.

First, create a format file `fmt.txt`:

```ruby
\n
Response Time for: %{url_effective}\n\n
DNS Lookup Time:\t\t%{time_namelookup}s\n
Redirection Time:\t\t%{time_redirect}s\n
Connection Time:\t\t%{time_connect}s\n
App Connection Time:\t\t%{time_appconnect}s\n
Pre-transfer Time:\t\t%{time_pretransfer}s\n
Start-transfer Time:\t\t%{time_starttransfer}s\n\n
Total Time:\t\t\t%{time_total}s\n
```

Variables used:
- `url_effective`: Final URL after redirects.
- `time_namelookup`: Time spent on DNS lookup.
- `time_redirect`: Time spent on redirects.
- `time_connect`: Time spent establishing TCP connection.
- `time_appconnect`: Time spent on SSL/SSH handshake.
- `time_pretransfer`: Time until the file transfer was about to begin.
- `time_starttransfer`: Time until the first byte was received.
- `time_total`: Total duration of the operation.

Execute the request:

```shell
curl -L -s -w @fmt.txt -o /dev/null http://www.example.com
```

#### **Requesting Compressed Response**

```shell
$ curl --compressed -o- -L https://yarnpkg.com/install.sh | bash
```
