tar
===

Save many files together into a single archive, and restore individual files from the archive.

## Description

The **tar command** (short for "tape archiver") is used to create and manipulate archives of files and directories in Linux. You can create archives for specific files, modify them, or add new files. While originally designed for tape backups, `tar` can now create archives on any device. It is extremely useful for bundling large numbers of files and directories into a single file for backup or network transfer.

It is important to distinguish between "archiving" and "compression". Archiving refers to bundling many files or directories into one combined file. Compression refers to reducing the size of a large file using specific algorithms.

Many Linux compression programs only work on a single file. Therefore, to compress a collection of files, you must first bundle them into a single archive using `tar`, and then compress that archive using tools like `gzip` or `bzip2`.

### Syntax

```shell
tar [options...] [FILE]...
```

### Options

```shell
-A, --catenate, --concatenate   Append tar files to an archive
-c, --create               Create a new archive
-d, --diff, --compare      Find differences between archive and file system
    --delete               Delete from archive (not for tapes!)
-r, --append               Append files to the end of an archive
-t, --list                 List the contents of an archive
    --test-label           Test the archive volume label and exit
-u, --update               Only append files newer than copy in archive
-x, --extract, --get       Extract files from an archive

Operation modifiers:

      --check-device         Check device numbers when creating incremental archives (default)
  -g, --listed-incremental=FILE   Handle new GNU-format incremental backup
  -G, --incremental          Handle old GNU-format incremental backup
      --ignore-failed-read   Do not exit with non-zero on unreadable files
      --level=NUMBER         Dump level for created listed-incremental archive
  -n, --seek                 Archive is seekable
      --no-check-device      Do not check device numbers when creating incremental archives
      --no-seek              Archive is not seekable
      --occurrence[=NUMBER]  Process only the NUMBERth occurrence of each file in the archive; 
                             this option is valid only in conjunction with one of the subcommands 
                             --delete, --diff, --extract or --list.
      --sparse-version=MAJOR[.MINOR]
                             Set version of the sparse format to use (implies --sparse)
  -S, --sparse               Handle sparse files efficiently

Overwrite control:

  -k, --keep-old-files       Don't replace existing files when extracting, treat them as errors
      --keep-directory-symlink   Preserve existing symlinks to directories when extracting
      --keep-newer-files     Don't replace existing files that are newer than their archive copies
      --no-overwrite-dir     Preserve metadata of existing directories
      --overwrite            Overwrite existing files when extracting
      --overwrite-dir        Overwrite metadata of existing directories when extracting (default)
      --recursive-unlink     Empty hierarchies prior to extracting directory
      --remove-files         Remove files after adding them to the archive
      --skip-old-files       Don't replace existing files when extracting, silently skip over them
  -U, --unlink-first         Remove each file prior to extracting over it
  -W, --verify               Attempt to verify the archive after writing it

Select output stream:

      --ignore-command-error Ignore exit codes of children
      --no-ignore-command-error
                             Treat non-zero exit codes of children as error
  -O, --to-stdout            Extract files to standard output
      --to-command=COMMAND   Pipe extracted files to another program

File attributes:

      --atime-preserve[=METHOD]
                             Preserve access times on dumped files, either by restoring the times
                             after reading (default METHOD='replace') or by not setting the times
                             in the first place (METHOD='system')
      --delay-directory-restore
                             Delay setting modification times and permissions of extracted
                             directories until the end of extraction
      --group=NAME           Force NAME as group for added files
      --mode=CHANGES         Force (symbolic) mode CHANGES for added files
      --mtime=DATE-OR-FILE   Set mtime for added files from DATE-OR-FILE
  -m, --touch                Don't extract file modification time
      --no-delay-directory-restore
                             Cancel the effect of --delay-directory-restore option
      --no-same-owner        Extract files as yourself (default for ordinary users)
      --no-same-permissions  Apply the user's umask when extracting permissions from the archive 
                             (default for ordinary users)
      --numeric-owner        Always use numbers for user/group names
      --owner=NAME           Force NAME as owner for added files
  -p, --preserve-permissions, --same-permissions
                             Extract information about file permissions (default for superuser)
      --preserve             Same as -p and -s
      --same-owner           Try extracting files with the same ownership as exists in the archive 
                             (default for superuser)
  -s, --preserve-order, --same-order
                             Member arguments are listed in the same order as the files in the archive

Handling of extended file attributes:

      --acls                 Enable the POSIX ACLs support
      --no-acls              Disable the POSIX ACLs support
      --no-selinux           Disable the SELinux context support
      --no-xattrs            Disable extended attributes support
      --selinux              Enable the SELinux context support
      --xattrs               Enable extended attributes support
      --xattrs-exclude=MASK  Specify the exclude pattern for xattr keys
      --xattrs-include=MASK  Specify the include pattern for xattr keys

Device selection and switching:

  -f, --file=ARCHIVE         Use archive file or device ARCHIVE
      --force-local          Archive file is local even if it has a colon
  -F, --info-script=NAME, --new-volume-script=NAME
                             Run script at end of each tape (implies -M)
  -L, --tape-length=NUMBER   Change tape after writing NUMBER x 1024 bytes
  -M, --multi-volume         Create/list/extract multi-volume archive
      --rmt-command=COMMAND  Use given rmt COMMAND instead of rmt
      --rsh-command=COMMAND  Use remote COMMAND instead of rsh
      --volno-file=FILE      Use/update the volume number in FILE

Device blocking:

  -b, --blocking-factor=BLOCKS   BLOCKS x 512 bytes per record
  -B, --read-full-records    Reblock as we read (for 4.2BSD pipes)
  -i, --ignore-zeros         Ignore zeroed blocks in archive (means EOF)
      --record-size=NUMBER   NUMBER bytes per record, multiple of 512

Archive format selection:

  -H, --format=FORMAT        Create archive of the given format

 FORMAT is one of the following:

    gnu                      GNU tar 1.13.x format
    oldgnu                   GNU format as per tar <= 1.12
    pax                      POSIX 1003.1-2001 (pax) format
    posix                    same as pax
    ustar                    POSIX 1003.1-1988 (ustar) format
    v7                       old V7 tar format

      --old-archive, --portability
                             Same as --format=v7
      --pax-option=keyword[[:]=value][,keyword[[:]=value]]...
                             Control pax keywords
      --posix                Same as --format=posix
  -V, --label=TEXT           Create archive with volume name TEXT; at list/extract time, 
                             use TEXT as a globbing pattern for volume name

Compression options:

  -a, --auto-compress        Use archive suffix to determine the compression program
  -I, --use-compress-program=PROG
                             Filter through PROG (must accept -d)
  -j, --bzip2                Filter the archive through bzip2
  -J, --xz                   Filter the archive through xz
      --lzip                 Filter the archive through lzip
      --lzma                 Filter the archive through lzma
      --lzop
      --no-auto-compress     Do not use archive suffix to determine the compression program
  -z, --gzip, --gunzip, --ungzip   Filter the archive through gzip
  -Z, --compress, --uncompress   Filter the archive through compress

Local file selection:

      --add-file=FILE        Add given FILE to the archive (useful if its name starts with a dash)
      --backup[=CONTROL]     Backup before removal, choose CONTROL version
  -C, --directory=DIR        Change to directory DIR
      --exclude=PATTERN      Exclude files matching PATTERN
      --exclude-backups      Exclude backup and lock files
      --exclude-caches       Exclude contents of directories containing CACHEDIR.TAG, 
                             except for the tag file itself
      --exclude-caches-all   Exclude directories containing CACHEDIR.TAG
      --exclude-caches-under Exclude everything under directories containing CACHEDIR.TAG
      --exclude-tag=FILE     Exclude contents of directories containing FILE, except for FILE itself
      --exclude-tag-all=FILE Exclude directories containing FILE
      --exclude-tag-under=FILE   Exclude everything under directories containing FILE
      --exclude-vcs          Exclude version control system directories
  -h, --dereference          Follow symlinks; archive and dump the files they point to
      --hard-dereference     Follow hard links; archive and dump the files they point to
  -K, --starting-file=MEMBER-NAME
                             Begin at member MEMBER-NAME when reading the archive
      --newer-mtime=DATE     Compare date and time when data changed only
      --no-null              Disable the effect of the previous --null option
      --no-recursion         Avoid descending automatically in directories
      --no-unquote           Do not unquote input file or member names
      --null                 -T reads null-terminated names, disable -C
  -N, --newer=DATE-OR-FILE, --after-date=DATE-OR-FILE
                             Only store files newer than DATE-OR-FILE
      --one-file-system      Stay in local file system when creating archive
  -P, --absolute-names       Don't strip leading '/'s from file names
      --recursion            Recurse into directories (default)
      --suffix=STRING        Backup before removal, override usual suffix ('~' unless overridden 
                             by environment variable SIMPLE_BACKUP_SUFFIX)
  -T, --files-from=FILE      Get names to extract or create from FILE
      --unquote              Unquote input file or member names (default)
  -X, --exclude-from=FILE    Exclude patterns listed in FILE

Filename transformations:

      --strip-components=NUMBER   Strip NUMBER leading components from file names on extraction
      --transform=EXPRESSION, --xform=EXPRESSION
                             Use sed replace EXPRESSION to transform file names

Informative output:

      --checkpoint[=NUMBER]  Display progress messages every NUMBERth record (default 10)
      --checkpoint-action=ACTION   Execute ACTION on each checkpoint
      --full-time            Print file time to its full resolution
      --index-file=FILE      Send verbose output to FILE
  -l, --check-links          Print a message if not all links are dumped
      --no-quote-chars=STRING   Disable quoting for characters from STRING
      --quote-chars=STRING   Add extra quoting characters from STRING
      --quoting-style=STYLE  Set name quoting style; see below for valid STYLE values
  -R, --block-number         Show block number within archive with each message
      --show-defaults        Show tar defaults
      --show-omitted-dirs    When listing or extracting, list each directory that does not match 
                             search criteria
      --show-transformed-names, --show-stored-names
                             Show transformed file or archive names
      --totals[=SIGNAL]      Print total bytes after processing the archive; with an argument - 
                             print total bytes when this SIGNAL is delivered; 
                             Allowed signals: SIGHUP, SIGQUIT, SIGINT, SIGUSR1 and SIGUSR2
      --utc                  Print file modification times in UTC
  -v, --verbose              Verbosely list files processed
  -w, --interactive, --confirmation
                             Ask for confirmation for every action
```

### Parameters

File or Directory: List of files or directories to be archived.

### Examples

Archive the `/home/vivek/bin/` directory and compress it using the `gzip` algorithm. Save it as `/tmp/bin-backup.tar.gz`.

```
tar -zcvf /tmp/bin-backup.tar.gz /home/vivek/bin/
```

```shell
- z: Filter through gzip
- j: Filter through bzip2
- Z: Filter through compress
- v: Verbosely show process
- O: Extract files to standard output
```

```shell
tar -cf archive.tar foo bar  # Create archive.tar from files foo and bar.
tar -tvf archive.tar         # List all files in archive.tar verbosely.
tar -xf archive.tar          # Extract all files from archive.tar.
```

The `-f` parameter is mandatory for specifying a file name and must be the last parameter.

```shell
tar -cf all.tar *.jpg
# Bundles all .jpg files into a package named all.tar. -c creates a new package, -f specifies the filename.

tar -rf all.tar *.gif
# Adds all .gif files to the existing all.tar. -r means append.

tar -uf all.tar logo.gif
# Updates logo.gif in the original all.tar. -u means update.

tar -tf all.tar
# Lists all files in all.tar. -t means list.
```

#### Compression Formats

**zip format**
Compress: `zip -r [target].zip [source]`
Extract: `unzip [source].zip`
Note: `-r` stands for recursive.

**tar format (Bundling only, no compression)**
Pack: `tar -cvf [target].tar [source]`
Unpack: `tar -xvf [source].tar`

**tar.gz format**
Method 1: Compress an existing tar file.
Compress: `gzip [source].tar`
Extract: `gunzip [source].tar.gz`

Method 2: Pack and compress in one step.
Pack and compress: `tar -zcvf [target].tar.gz [source]`
Extract and unpack: `tar -zxvf [source].tar.gz`

**tar.bz2 format**
Pack and compress: `tar -jcvf [target].tar.bz2 [source]`
Extract and unpack: `tar -jxvf [source].tar.bz2`
Note: `-j` uses the `bzip2` algorithm.

**tar.xz format**
Pack and compress: `tar -Jcvf [target].tar.xz [source]`
Extract and unpack: `tar -Jxvf [source].tar.xz`
Note: `-J` uses the `xz` algorithm.

**tar.Z format (Obsolete)**
Pack and compress: `tar -Zcvf [target].tar.Z [source]`
Extract and unpack: `tar -Zxvf [source].tar.Z`

**jar format**
Compress: `jar -cvf [target].jar [source]`
Extract: `jar -xvf [source].jar`

**7z format**
Compress: `7z a [target].7z [source]`
Extract: `7z x [source].7z`
Note: `7z` also supports `rar` extraction: `7z x source.rar`

#### Other Examples

**Create archives**:
```shell
tar -cvf log.tar log2012.log    # Bundling only, no compression
tar -zcvf log.tar.gz log2012.log # Bundle and compress with gzip
tar -jcvf log.tar.bz2 log2012.log # Bundle and compress with bzip2
```

**Strip components on extraction**:
Use `--strip-components NUMBER` to remove leading directory levels.
```shell
tar -xvf portal-web-v2.0.0.tar --strip-components 1 -C /target/dir
```

**List files in an archive**:
```shell
tar -ztvf log.tar.gz
```

**Extract specific files**:
```shell
tar -zxvf /opt/soft/test/log30.tar.gz log2013.log
```

**Backup and preserve permissions**:
```shell
tar -zcvpf log31.tar.gz log2014.log log2015.log
```
The `-p` attribute is important for preserving file attributes.

**Backup files newer than a specific date**:
```shell
tar -N "2012/11/13" -zcvf log17.tar.gz test
```

**Exclude files/directories**:
```shell
tar --exclude scf/service -zcvf scf.tar.gz scf/*
```

**Remove source files after archiving**:
```shell
tar -cvf test.tar test --remove-files
```

**Core usage summary**:
```shell
Compress: tar -jcv -f filename.tar.bz2 [source]
List:     tar -jtv -f filename.tar.bz2
Extract:  tar -jxv -f filename.tar.bz2 -C [target_dir]
```
