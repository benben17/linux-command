pvdisplay
===

Display physical volume attributes.

## Description

The **pvdisplay command** is used to display the attributes of physical volumes. The information shown includes: physical volume name, the volume group it belongs to, physical volume size, PE size, total number of PEs, free PEs, allocated PEs, and UUID.

### Syntax

```shell
pvdisplay(options)(parameters)
```

### Options

```shell
-s: Output in short format;
-m: Display mapping of PEs to LEs.
```

### Parameters

Physical Volume: The device file name of the physical volume to be displayed.

### Example

Use the `pvdisplay` command to show basic information for a specified physical volume. Enter the following command:

```shell
[root@localhost ~]# pvdisplay /dev/sdb1    # Display basic physical volume info
```

Output information:

```shell
"/dev/sdb1" is a new physical volume of "101.94 MB"  
--- NEW Physical volume ---  
PV Name               /dev/sdb1  
....part of output omitted......  
PV UUID         FOXiS2-Ghaj-Z0Mf- cdVZ-pfpk- dP9p-ifIZXN
```
