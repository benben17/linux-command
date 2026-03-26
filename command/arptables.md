arptables
===

Manage ARP packet filtering rule tables

## Additional Information

The **arptables command** is used to set up, maintain, and inspect the ARP packet filtering rule tables in the Linux kernel.

### Syntax

```shell
arptables (options)
```

### Options

```shell
-A: Append a rule to a rule chain.
-D: Delete a rule from a specified chain.
-I: Insert a new rule into a rule chain.
-R: Replace a specified rule.
-P: Set the default policy for a rule chain.
-F: Flush the specified rule chain, deleting all rules within it without changing the default policy.
-Z: Zero the counters for a rule chain.
-L: List the rules in a rule chain.
-X: Delete the specified empty user-defined rule chain.
-h: Display command help information.
-j: Specify the target for the matching rule.
-s: Specify the source IP address to match in the ARP packet.
-d: Specify the destination IP address to match in the ARP packet.
```
