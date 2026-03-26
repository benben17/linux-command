pvs
===

Output a report of physical volume information.

## Description

The **pvs command** is used to output a formatted report of physical volume information. It provides a summary of physical volumes; for more detailed information, use the `pvdisplay` command.

### Syntax

```shell
pvs(options)(parameters)
```

### Options

```shell
--noheadings: Do not output column headers;
--nosuffix: Do not output units for space sizes.
```

### Parameters

Physical Volume: A list of physical volumes for which to display the report.

### Example

Use the `pvs` command to display a report of all physical volumes in the system. Enter the following command:

```shell
pvs # Output physical volume information report 
```

Output information:

```shell
PV         VG     fmt  Attr PSize   PFree  
/dev/sdb1  vg1000 lvm2 --   100.00M 100.00M  
/dev/sdb2         lvm2 --   101.98M 101.98M
```
