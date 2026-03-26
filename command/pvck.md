pvck
===

Check LVM metadata consistency on a physical volume.

## Description

The **pvck command** is used to check the consistency of LVM metadata on a physical volume. By default, the LVM label is stored in the first 4 sectors. The `--labelsector` option can be used to specify a different location (e.g., during data recovery).

### Syntax

```shell
pvck(options)(parameters)
```

### Options

```shell
-d: Debug mode;
-v: Verbose mode;
--labelsector: Specify the sector where the LVM label is located.
```

### Parameters

Physical Volume: Specifies the device file for the physical volume to be checked.

### Example

Use the `pvck` command to check the physical volume `/dev/sdb1`. Enter the following command:

```shell
pvck -v /dev/sdb1    # Check physical volume metadata
Scanning /dev/sdb1  
Found label on /dev/sdb1, sector 1, type=LVM2 001  
Found text metadata area: offset=4096, size=192512 
Found LVM2 metadata record at offset=125952,  
size=70656, offset2=0 size2=0
```
