iptstate
===

Display iptables state information in a top-like interface.

## Description

The `iptstate` command displays the state of netfilter/iptables connections in the Linux kernel in a style similar to the `top` command.

### Syntax

```shell
iptstate [options]
```

### Options

```shell
-b : Specify sorting criteria for the output.
-d : Do not dynamically resize the window.
-f : Filter loopback information.
-l : Resolve IP addresses to hostnames.
-L : Hide DNS query-related states.
-r : Set the screen refresh rate.
-R : Reverse sort order.
-s : Single run mode (non-interactive).
-t : Display summary information.
```
