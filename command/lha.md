lha
===

Compress or decompress LZH format files

## Description

The **lha** command is a compression program evolved from `lharc`. Files compressed with it will have the `.lzh` extension.

### Options

```shell
-a or a: Compress files and add them to the archive.
-a<0/1/2>/u</0/1/2>: Use different header levels when compressing.
-c or c: Re-create the archive and add the compressed files.
-d or d: Delete specified files from the archive.
-<a/c/u>d or <a/c/u>d: Compress and add files, then delete the original files (move to archive).
-e or e: Extract files from the archive.
-f or f: Force execution; overwrite existing files during extraction without prompting.
-g or g: Use generic format for compatibility.
-<e/x>i or <e/x>i: Ignore the stored paths when extracting; extract files to the current or specified directory.
-l or l: List the contents of the archive.
-m or m: Same as the "-ad" option (move to archive).
-n or n: No action; only list what would be performed.
-<a/u>o or <a/u>o: Use lharc compatible format when adding or updating files.
-p or p: Extract files to standard output.
-q or q: Quiet mode; do not display the execution process.
-t or t: Test the integrity of each file in the backup/archive.
-u or u: Update the archive with newer versions of files.
-v or v: List the contents of the archive with detailed information.
-<e/x>w=<dir> or <e/x>w=<dir>: Specify the destination directory for extraction.
-x or x: Extract files from the archive.
-<a/u>z or <a/u>z: Add or update files in the archive without compression.
```

### Examples

```shell
lha -a abc.lhz a.b         # Compress file a.b into abc.lhz
lha -a abc2 /home/hnlinux  # Compress a directory
lha -xiw=agis abc          # Extract file abc to the current directory
```
