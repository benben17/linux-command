jwhois
===

A client for the Whois service.

## Description

`jwhois` searches Whois servers for information about objects specified on the command line. It is a configuration-driven whois client that can automatically select the correct server to query based on domain names, IP addresses, or other identifiers.

### Syntax

```shell
jwhois [options] [query]
```

### Options

```shell
--version                  Display version number and patch level.
--help                     Display help information.
-v, --verbose              Enable verbose debug output.
-c FILE, --config=FILE     Use FILE as the configuration file.
-h HOST, --host=HOST       Explicitly query the specified HOST.
-n, --no-redirect          Disable content redirection.
-s, --no-whoisservers      Disable whois-servers.net service support.
-a, --raw                  Disable reformatting of the query results.
-i, --display-redirections Display all redirects instead of hiding them.
-p PORT, --port=PORT       Use the specified port number (with HOST).
-r, --rwhois               Force an rwhois query.
--rwhois-display=DISPLAY   Set the display option in rwhois queries.
--rwhois-limit=LIMIT       Set the maximum number of matches to return.
```

### Examples

**Query information for a user:**
```shell
jwhois root
```

**Query domain information:**
```shell
jwhois example.net
```
