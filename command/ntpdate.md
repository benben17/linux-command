ntpdate
===

Set the date and time using the Network Time Protocol (NTP).

## Description

The **ntpdate command** is used to set the local date and time. It polls the specified NTP servers to obtain a set of samples and applies the standard NTP clock filter and selection algorithms to choose the best sample.

The ntpdate command adjusts the clock using the following methods:

*   If the clock offset is greater than 0.5 seconds, it sets the clock time directly by calling the `settimeofday` subroutine. This is the preferred method at boot time.
*   If the clock offset is less than 0.5 seconds, it adjusts the clock time by calling the `adjtime` subroutine with the offset. This method tends to maintain the drift clock more accurately at the expense of some stability. When ntpdate is run regularly from a cron command (e.g., every one or two hours) instead of running a daemon, it can ensure sufficient accuracy and avoid abrupt clock steps.

Using multiple servers significantly improves the reliability and accuracy of the ntpdate command. Although a single server can be used, providing at least three or four servers will yield better performance.

If an NTP daemon like `xntpd` is already running on the same host, ntpdate will refuse to set the date.

You must have root privileges to run this command.

### Syntax

```shell
ntpdate [ -b] [ -d] [ -s] [ -u] [ -aKeyid] [ -eAuthenticationDelay] [ -kKeyFile] [ -oVersion] [ -pSamples] [ -tTimeOut] Server...
```

### Options

```shell
-aKeyid               # Use Keyid to authenticate all packets.
-b                    # Force the time to be stepped using the settimeofday subroutine.
-d                    # Enable debug mode. Determine what ntpdate would do without actually setting the clock. Results are displayed on the screen. This flag uses unprivileged ports.
-eAuthenticationDelay # Specify the processing delay for authentication in seconds.
-kKeyFile             # Specify a different name for the key file instead of the default /etc/ntp.keys.
-oVersion             # Specify the NTP version to use (1, 2, or 3). The default is 3.
-pSamples             # Specify the number of samples to acquire from each server (between 1 and 8). The default is 4.
-s                    # Log messages to the syslog facility instead of standard output. Useful when running ntpdate via cron.
-tTimeOut             # Specify the timeout for waiting for a response. The value is rounded to the nearest multiple of 0.2 seconds. The default is 1 second.
-u                    # Use an unprivileged port for outgoing packets. This is useful when behind a firewall that blocks incoming traffic to privileged ports.
-q                    # Query only - do not set the clock.
```
