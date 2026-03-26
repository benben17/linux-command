zip
===

Package and compress (archive) files

## Description

The **zip** command is used to package and compress files into an archive. zip is a widely used compression utility; files compressed with it will have a ".zip" extension.

### Syntax

```shell
zip [options] [parameters]
zip [-options] [-b path] [-t date] [-n suffixes] [zipfile list] [-xi list]
```

### Options

```shell
-f, --freshen: Freshen: only changed files
-u, --update: Update: only changed or new files
-d, --delete: Delete entries in zip file
-m, --move: Move into zip file (delete OS files)
-r, --recurse-paths: Recurse into directories
-j, --junk-paths: Junk (don't record) directory names
-0, --store: Store only
-l, --lf-to-crlf: Convert LF to CR LF (-ll for CR LF to LF)
-1: Faster compression
-9: Better compression
-v, --verbose: Verbose operation/print version info
-q, --quiet: Quiet operation
-c, --entry-comments: Add a one-line comment
-z, --archive-comment: Add zip file comment
-@, --names-stdin: Read names from standard input
-o, --latest-time: Make zip file as old as latest entry
-x, --exclude: Exclude the following names
-i, --include: Include only the following names
-F, --fix: Fix zip file (-FF for more effort)
-D, --no-dir-entries: Do not add directory entries
-A, --adjust-sfx: Adjust self-extracting exe
-T, --test: Test zip file integrity
-X, --no-extra: Exclude extra file attributes
-n, --suffixes: Do not compress these suffixes
-e, --encrypt: Encrypt
-y, --symlinks: Store symbolic links as links rather than referenced files
-h2, --help-more: Show more help
```

### Parameters

*   zip package: Specifies the zip archive to be created;
*   file list: Specifies the list of files to be compressed.

### Examples

Compress a single file, which will compress `file.txt` into an archive named `compressed.zip`:

```shell
zip compressed.zip file.txt
```

Compress multiple files, this command will compress `file1.txt`, `file2.txt`, and `file3.txt` into an archive named `compressed.zip`:

```shell
zip compressed.zip file1.txt file2.txt file3.txt
```

Compress an entire directory, the `-r` parameter indicates recursive compression; this command will compress the `folder` directory and all its subdirectories and files:

```shell
zip -r compressed.zip folder/
```

Compress files using the maximum compression ratio, the `-9` parameter specifies the maximum compression ratio, although it may take longer:

```shell
zip -9 compressed.zip file.txt
```

Create a password-protected zip file, the `-e` parameter will prompt the user to enter a password to create an encrypted zip file:

```shell
zip -e secure.zip file.txt
```

Only compress new or changed files, if `compressed.zip` already exists, the `-u` parameter will update `file.txt` in the archive or add it to the archive if it is new:

```shell
zip -u compressed.zip file.txt
```

Compress files without preserving the directory structure, the `-j` parameter will not preserve the parent directory `folder` of `file.txt`; the file will be located at the root of the zip file:

```shell
zip -j compressed.zip folder/file.txt
```

Package all files and folders in the `/home/Blinux/html/` directory into `html.zip` in the current directory:

```shell
zip -q -r html.zip /home/Blinux/html
```

The above command compresses files and folders using absolute paths. To use relative paths (e.g., if you are currently in the `Blinux` directory), perform the following to achieve the same result:

```shell
zip -q -r html.zip html
```

If you are currently in the `html` directory, use the following zip command:

```shell
zip -q -r html.zip *
```

Compress the contents of the `example/basic/` directory into `basic.zip`, excluding certain directories using `-x` (note that it will not work without double quotes):

```shell
zip -r basic.zip example/basic/ -x "example/basic/node_modules/*" -x "example/basic/build/*" -x "example/basic/coverage/*"
```

The above command compresses and extracts content into `example/basic/`. If you want to store it in the root directory, enter the directory before compressing. Currently, there is no single parameter to solve this problem directly.

```shell
cd example/basic/ && zip -r basic.zip . -x "node_modules/*" -x "build/*" -x "coverage/*"
```

Choosing compression efficiency:

```shell
zip -9 # 1-9 faster->better
```

Create a zip of the `public_html` directory while ignoring all files and folders that contain the text `backup`:

```shell
zip -r public_html.zip public_html -x *backup*
```

Create an archive of all files in the `httpdocs` directory while ignoring `.svn` or `git` files and directories:

```shell
zip -r httpdocs.zip httpdocs --exclude *.svn* --exclude *.git*
```

Create an archive of all files in the `httpdocs` directory while ignoring all files ending with `.log`:

```shell
zip -r httpdocs.zip httpdocs --exclude "*.log"
```

### Troubleshooting

Command not found in CentOS 7:

```shell
-Bash: Unzip: Command Not Found
```

Solution:

```shell
yum install -y unzip zip
```
