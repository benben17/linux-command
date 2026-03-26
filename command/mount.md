mount
===

Used to mount filesystems

## Description

The **mount command** is a frequently used tool in Linux for mounting external filesystems or devices onto the system's directory tree.

To mount a network drive via the WebDAV protocol, you need to install the necessary components by running `apt install davfs2`.

### Syntax

```shell
mount [-hV]
mount -a [-fFnrsvw] [-t vfstype]
mount [-fnrsvw] [-o options [,...]] device | dir
mount [-fnrsvw] [-t vfstype] [-o options] device dir
```

### Options

```shell
-V: Display version information.
-h: Display help message.
-v: Verbose mode, often used with -f for debugging.
-a: Mount all filesystems defined in /etc/fstab.
-F: Usually used with -a, it forks a new process for each mount. This speeds up mounting large numbers of NFS filesystems.
-f: Fake mount. It doesn't actually mount the filesystem but simulates the process. Often used with -v for debugging.
-n: Mount without writing to /etc/mtab. Useful when the root filesystem is read-only.
-s -r: Equivalent to -o ro (read-only).
-w: Equivalent to -o rw (read-write).
-L: Mount the partition with the specified label.
-U: Mount the partition with the specified UUID. -L and -U require /proc/partitions to exist.
-t: Specify the filesystem type. Usually, mount automatically detects the correct type.
-o async: Enable asynchronous mode; all I/O operations are performed asynchronously.
-o sync: Enable synchronous mode; all I/O operations are performed synchronously.
-o atime, -o noatime: Update/don't update the last access time for files. "noatime" is often used with flash storage to reduce writes.
-o auto, -o noauto: Enable/disable automatic mounting (e.g., via mount -a).
-o defaults: Use default options: rw, suid, dev, exec, auto, nouser, and async.
-o dev, -o nodev: Interpret/don't interpret character or block special devices on the filesystem.
-o exec, -o noexec: Allow/disallow execution of binaries on the filesystem.
-o suid, -o nosuid: Respect/ignore set-user-identifier or set-group-identifier bits.
-o user, -o nouser: Allow/disallow ordinary users to mount/umount the filesystem.
-o remount: Remount an already mounted filesystem with different options (e.g., changing from ro to rw).
-o ro: Mount as read-only.
-o rw: Mount as read-write.
-o loop: Use loop device to mount a file as a filesystem (e.g., ISO images).
```

### Example 1

Mount `/dev/hda1` to `/mnt`.

```shell
mount /dev/hda1 /mnt
```

Mount `/dev/hda1` in read-only mode to `/mnt`.

```shell
mount -o ro /dev/hda1 /mnt
```

Mount an ISO image `/tmp/image.iso` to `/mnt/cdrom` using loop mode. This allows you to view the contents of a Linux ISO without burning it to a disc.

```shell
mount -o loop /tmp/image.iso /mnt/cdrom
```

### Example 2
Mount a network drive via WebDAV protocol.

Mount the network storage at `https://your.webdav.link.here` to the local path `/path/to/mount`.

```shell
mount -t davfs https://your.webdav.link.here /path/to/mount
```

### Example 3
Mount an Android system partition to `/dev/loopX`. You can specify the filesystem type with `-t` (e.g., `ext4`) if known.

```shell
mount -t ext4 /dev/loopX /mnt/system
```
