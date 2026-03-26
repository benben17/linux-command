znew
===

Convert .Z archives to .gz archives

## Description

The **znew** command is used to re-compress files from the compress (.Z) format to the gzip (.gz) format.

### Syntax

```shell
znew [options] [parameters]
```

### Options

```shell
-f, --force: Force conversion even if the target .gz file already exists;
-t, --test: Test the new files before deleting the originals;
-v, --verbose: Display filenames and compression ratios for each file;
-9, --best: Use the maximum compression ratio (slower);
-P, --pipe: Use pipes for the conversion to reduce disk space usage;
-K, --keep: Keep the original .Z file if it is smaller than the .gz file.
```

### Parameters

File: Specifies the .Z archive created by the compress command.
