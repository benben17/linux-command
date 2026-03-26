pvremove
===

Remove an existing physical volume.

## Description

The **pvremove command** is used to remove an existing physical volume. When deleting a physical volume, it wipes the LVM metadata on the partition so it is no longer recognized as a physical volume.

### Syntax

```shell
pvremove(options)(parameters)
```

### Options

```shell
-d # Debug mode;
-f # Force removal;
-y # Answer "yes" to all questions.
```

### Parameters

Physical Volume: Specifies the device file name of the physical volume to be removed.

### Example

Use the `pvremove` command to delete the physical volume `/dev/sdb2`. Enter the following command:

```shell
pvremove /dev/sdb2 # Remove physical volume
Labels on physical volume "/dev/sdb2" successfully wiped
```
