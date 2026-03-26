restore
===

The reverse operation of the `dump` command.

## Description

The **restore command** is the inverse of the `dump` command, used to restore backup files created by the `dump` command. While dumping is used for backing up files, restoration is the process of writing these backed-up files back to the system.

### Syntax

```shell
restore(options)
```

### Options

```shell
-b<block_size>: Sets the block size in bytes.
-c: Does not check the dump format; only allows reading backup files in the old format.
-C: Comparison mode; compares the backup files with the current files.
-D<filesystem>: Allows the user to specify the name of the filesystem.
-f<backup_file>: Reads backup data from the specified file for restoration.
-h: Extracts only the directory itself, excluding all files related to that directory.
-i: Interactive mode; the restore command will prompt the user sequentially during restoration.
-m: Extracts files or directories matching specified inode numbers instead of filenames.
-r: Performs the restoration operation.
-R: When restoring the entire filesystem, checks where the restoration should begin.
-s<file_number>: When backup data spans multiple tapes, specifies the backup file number.
-t: Lists the names of the specified files if they exist in the backup.
-v: Displays detailed information during command execution.
-x: Extracts specified files from the storage medium and restores them to the filesystem if they exist in the backup.
-y: Does not prompt for confirmation; assumes "yes" to all questions and continues.
```

### Examples

Create a backup using the `dump` command:

```shell
dump -9 -u -f /dev/hda3 /home/frank/
```

Restore the backup using the `restore` command:

```shell
restore rf /dev/hda3 /home/frank
```

View the list of files in the backup using the `restore` command:

```shell
restore ft /dev/hda3
```
