axel
===

Multi-threaded download tool

## Additional Information

**axel** is an excellent HTTP/FTP high-speed download tool for Linux. It supports multi-threaded downloads and resuming downloads, and can download the same file from multiple addresses or multiple connections from a single address. It is suitable for increasing download speeds when network conditions are poor. For example, using Axel to download LNMP one-click installation packages on a domestic VPS or server is faster than using `wget`.

### Installation

#### Source Installation

GitHub address: https://github.com/axel-download-accelerator/axel

After downloading the corresponding release version, extract it, enter the directory, and execute `./configure && make && make install` to install.

#### Binary Installation

Install Axel on CentOS:

Axel is currently not in the yum repositories. You can download the RPM package from http://pkgs.repoforge.org/axel/ for installation.

For 32-bit CentOS, run:

```shell
wget -c http://pkgs.repoforge.org/axel/axel-2.4-1.el5.rf.i386.rpm
rpm -ivh axel-2.4-1.el5.rf.i386.rpm
```

For 64-bit CentOS, run:

```shell
wget -c http://pkgs.repoforge.org/axel/axel-2.4-1.el5.rf.x86_64.rpm
rpm -ivh axel-2.4-1.el5.rf.x86_64.rpm
```

Install Axel on Debian/Ubuntu:

```shell
apt-get install axel
```

### Syntax

```shell
axel [options] url1 [url2] [url...]
```

### Options

```shell
--max-speed=x , -s x         # Maximum speed x
--num-connections=x , -n x   # Number of connections x
--output=f , -o f            # Save as local file f
--search[=x] , -S [x]        # Search for mirrors
--header=x , -H x            # Add header string x (specify HTTP header)
--user-agent=x , -U x        # Set user agent (specify HTTP user agent)
--no-proxy , -N              # Do not use proxy server
--quiet , -q                 # Quiet mode
--verbose , -v               # More status information
--alternate , -a             # Alternate progress indicator
--help , -h                  # Help
--version , -V               # Version information
--insecure , -k              # Do not verify SSL certificates
```

### Examples

Download an LNMP installation package with 10 threads and save it to `/tmp/`:

```shell
axel -n 10 -o /tmp/ http://www.jsdig.com/lnmp.tar.gz
```

If the download is interrupted, simply execute the download command again to resume from where it left off.
