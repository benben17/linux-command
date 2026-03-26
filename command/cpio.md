cpio
===

A tool for creating and restoring backup archives

## Description

The **cpio command** is primarily used as a utility for creating or restoring backup archives. It can copy files into an archive or extract files from an existing one.

### Syntax

```shell
cpio [options]
```

### Options

```shell
-0 or --null: Read a list of filenames terminated by a null character instead of a newline. Often used with 'find -print0'.
-a or --reset-access-time: Reset the access times of files after reading them.
-A or --append: Append to an existing archive. The archive must be on a disk, not a tape.
-b or --swap: Swap both halfwords of words and bytes of halfwords. Same as -ss.
-B: Set the I/O block size to 5120 bytes.
-c: Use the old portable (ASCII) archive format.
-C <size> or --io-size=<size>: Set the I/O block size to <size> bytes.
-d or --make-directories: Create leading directories where needed.
-E <file> or --pattern-file=<file>: Read patterns for matching filenames from <file>.
-f or --nonmatching: Extract only files that do not match the given patterns.
-F <archive> or --file=<archive>: Use <archive> instead of standard input or output.
-H <format>: Use the specified archive format.
-i or --extract: Run in copy-in mode (extract from archive).
-l <archive>: Specify the archive name instead of standard input.
-k: Ignored; exists for compatibility with different cpio versions.
-l or --link: Link files instead of copying them, where possible (copy-pass mode).
-L or --dereference: Copy the file pointed to by a symbolic link instead of the link itself.
-m or --preserve-modification-time: Retain previous file modification times when creating files.
-M <message> or --message=<message>: Print <message> when the end of a volume is reached.
-n or --numeric-uid-gid: Show numeric UID and GID instead of names in 'cpio -tv'.
-o or --create: Run in copy-out mode (create archive).
-O <archive>: Use <archive> instead of standard output.
-p or --pass-through: Run in copy-pass mode (copy files directly to a destination directory).
-r or --rename: Interactively rename files.
-R <user>[:<group>] or --owner <user>[:<group>]: Set the ownership of files in copy-in or copy-pass mode.
-s or --swap-bytes: Swap bytes of each halfword in the files.
-S or --swap-halfwords: Swap halfwords of each word in the files.
-t or --list: Print a table of contents of the input.
-u or --unconditional: Replace all files without asking, regardless of modification time.
-v or --verbose: List the files processed.
-V or --dot: Print a "." for each file processed.
--block-size=<size>: Set the I/O block size.
--force-local: Force the archive file to be local, even if it has a colon.
--help: Display help information.
--no-absolute-filenames: Create all files relative to the current directory.
--no-preserve-owner: Do not preserve file ownership.
--only-verify-crc: When using the CRC format, verify the CRC of each file.
--quiet: Do not print the number of blocks copied.
--sparse: Create sparse files for files containing large sequences of null bytes.
--version: Display version information.
```

### Examples

**Back up all regular files in `/etc` to `/opt/etc.cpio`:**

```shell
find /etc -type f | cpio -ocvB > /opt/etc.cpio
```

**Back up all data on the system to a tape drive:**

```shell
find / -print | cpio -covB > /dev/st0
```

Here, `/dev/st0` is the device name for a SCSI tape drive.

**View the files backed up on the tape drive in the previous example:**

```shell
cpio -icdvt < /dev/st0 > /tmp/st_content
```

If there are too many files to display on one screen, you can redirect the output to a file.

**Restore the backup from the first example to its original location, overwriting existing files:**

```shell
cpio -icduv < /opt/etc.cpio
```

Note: `cpio` restores files based on the paths used during archiving. If absolute paths were used, files will be restored to those absolute paths. If relative paths were used, they will be restored relative to the current directory.

As seen in these examples, `cpio` cannot read files directly; it requires a list of full pathnames, which is exactly what the `find` command provides. Therefore, `cpio` is commonly used in conjunction with `find`.
观察
