vdfuse
===

A tool for mounting VirtualBox VDI partition files.

## Description

The **vdfuse command** is a tool for mounting VirtualBox VDI partition files. VirtualBox is an open-source software for creating virtual machines, and VDI is its default disk format.

### What is VirtualBox?

VirtualBox is a powerful x86 virtualization software that is rich in features and delivers excellent performance. Furthermore, VirtualBox went open-source several years ago and is now free software released under the GPL license. VirtualBox can run on Linux and Windows hosts and supports installing guest operating systems from the Windows (NT 4.0, 2000, XP, Server 2003, Vista), DOS/Windows 3.x, Linux (2.4 and 2.6), and OpenBSD series.

 **To install vdfuse on Ubuntu, open the terminal and enter:** 

```shell
sudo apt-get install virtualbox-fuse
```

### Syntax

```shell
vdfuse [options] -f image-file mountpoint
```

### Options

```shell
-h: Help;
-r: Read-only;
-t: Type (VDI, VMDK, VHD, or raw; default: auto);
-f: Image file;
-a: Allow all users to read;
-w: Allow all users to write;
-g: Run in the foreground;
-v: Output feedback;
-d: Debug mode.
```

Note: You must edit `/etc/fuse.conf` and uncomment "user_allow_other" (remove the #), otherwise it will not run correctly.

### Examples

Use the following statement to mount a .vdi file:

```shell
sudo vdfuse -f /path/to/file.vdi /path/to/mountpoint
```

`/path/to/mountpoint` should contain files such as `EntireDisk`, `Partition1`, etc. If there is only one file, you may need to mount it like this:

```shell
mount /path/to/mountpoint/Partition1 /path/to/someother/mountpoint
```

The file system is then mounted at `/path/to/someother/mountpoint`.
