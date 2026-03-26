e2label
===

Set the label of an ext2, ext3, or ext4 file system.

## Description

The **e2label** command is used to set the label of a second extended file system.

### Syntax

```shell
e2label [parameters]
```

### Parameters

*   File system: Specify the device file name corresponding to the file system;
*   New label: Specify a new label for the file system.

### Examples

Many people who have used Linux for years may have never used the `e2label` command, but it is quite effective. Before introducing it, let's look at the `/etc/fstab` file:

```shell
LABEL=/ / ext3 defaults 1 1
/dev/hda7 /usr ext3 defaults 1 1
```

The meaning of the second line is easy to understand: mount `/dev/hda7` to `/usr`. The first line does not specify a partition; it means mount the partition with the label `/` to `/`. The advantage of writing it this way is that even if the hard disk is moved from `ide0 (hda)` to `ide2 (hdc)` on the motherboard, the system can still automatically mount the correct partition. Usually, the label is automatically assigned when Linux is installed. If a new partition is added manually, you can use the following command to assign a label to it:

```shell
e2label /dev/hdax /new
mkdir /new
```

Then add it to `/etc/fstab`:

```shell
LABEL=/new  /new  ext3  defaults  1 1
```

The next time the machine is restarted, the partition with the label `/new` will be mounted to `/new`.
