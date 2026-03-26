mkisofs
===

Create an ISO 9660 image file

## Description

The **mkisofs command** is used to create an ISO 9660 filesystem image from a specified directory and its files. This image can then be burned onto a CD or DVD.

### Syntax

```shell
mkisofs [OPTION]... [PATH]
```

### Options

```shell
-a, --all：Include backup files in the image.
-A <id>：Specify the application ID.
-abstract <file>：Specify the abstract file name.
-b <image>：Specify the boot image for creating bootable El Torito CDs.
-c <name>：Specify the boot catalog name for bootable CDs.
-C <last_sess_start,next_sess_start>：Needed when creating a multi-session image.
-copyright <file>：Specify the copyright file name.
-d, -omit-period：Omit trailing periods from filenames.
-D, -disable-deep-relocation：Disable deep directory relocation (ISO 9660 allows only 8 levels).
-f, -follow-links：Follow symbolic links.
-h：Display help.
-hide <glob>：Hide specified files or directories from the ISO 9660/Rock Ridge directory.
-J, -joliet：Generate Joliet directory records for Windows systems.
-l, -full-iso9660-filenames：Allow full 31-character ISO 9660 filenames.
-L, -allow-leading-dots：Allow filenames to begin with a period.
-o <file>：Specify the output image filename.
-p <preparer>：Specify the volume preparer ID.
-print-size：Print the estimated size of the resulting filesystem.
-quiet：Quiet execution; suppress all output.
-r, -rational-rock：Use Rock Ridge extensions and set reasonable file permissions.
-R, -rock：Use Rock Ridge extensions.
-v, -verbose：Verbose mode.
-V <id>：Specify the volume ID.
-x <dir>：Exclude the specified directory from the image.
```

### Parameters

Path: The directory or files to include in the ISO image.

### Examples

Steps to create an ISO from a directory:

1. Mount a remote directory (optional):
```shell
mount -t nfs 10.0.2.2:/linuxos/rhel4.0/ /mnt/nfs/
```

2. Copy files to a local staging area:
```shell
cp -a /mnt/nfs/* /root/Desktop/rhel4.0/
```

3. Clean up unnecessary files:
```shell
find rhel4.0/ -name boot.cat | xargs rm
find rhel4.0/ -name TRANS.TBL -exec rm {} \;
```

4. Create the ISO image:
```shell
mkisofs -R -J -T -v -no-emul-boot -boot-load-size 4 -boot-info-table -V RHEL4ASDVD -b isolinux/isolinux.bin -c isolinux/boot.cat -o /RHEL4AS.iso rhel4.0/
```
