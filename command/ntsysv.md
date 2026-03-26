ntsysv
===

Centrally manage various system services.

## Description

The **ntsysv command** provides a text-based menu interface for centrally managing the startup status of system services across different runlevels. This tool is included by default in various Red Hat distributions and CentOS versions. It features an interactive interface where you can easily use the arrow keys and the spacebar to enable or disable system services for each execution level.

### Syntax

```shell
ntsysv(options)
```

### Options

```shell
--level <levels>: Specify the runlevels to configure (e.g., --level 35).
--back: Display a "Back" button instead of a "Cancel" button in the interactive interface.
```

### Examples

After entering the `ntsysv` command, an interactive management menu will appear:

```shell
ntsysv
```

Use the **Spacebar** to select or deselect options!
