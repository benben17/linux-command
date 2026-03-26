du
===

Display disk usage for each file and directory.

## Description

The **du** command is also used to check space usage, but unlike the `df` command, the Linux `du` command is used to view the space used by files and directories. There are some differences between it and the `df` command.

### Syntax

```shell
du [OPTION]... [FILE]...
```

### Options

```shell
-a, --all                              Show sizes for individual files in directories.
-B, --block-size=SIZE                  Use SIZE-byte blocks.
-b, --bytes                            Display directory or file sizes in bytes.
-c, --total                            Produce a grand total.
-D, --dereference-args                 Dereference FILEs that are symbolic links.
-d, --max-depth=N                      Limit folder depth.
-H, --si                               Same as -h, but use powers of 1000 (K, M, G).
-h, --human-readable                   Print sizes in human readable format (e.g., 1K 234M 2G).
-k, --kilobytes                        Like --block-size=1K.
-l, --count-links                      Count sizes many times if hard linked.
-m, --megabytes                        Like --block-size=1M.
-L, --dereference                      Dereference all symbolic links.
-P, --no-dereference                   Don't follow any symbolic links (default).
-0, --null                             End each output line with NUL, not newline.
-S, --separate-dirs                    For directories do not include size of subdirectories.
-s, --summarize                        Display only a total for each argument.
-x, --one-file-system                  Skip directories on different file systems.
-X, --exclude-from=FILE                Exclude files that match any pattern in FILE.
--apparent-size                        Print apparent sizes, rather than disk usage; although the apparent size is usually smaller, it may be larger due to holes in ('sparse') files, internal fragmentation, indirect blocks, and the like.
--files0-from=F                        Summarize disk usage of the NUL-terminated file names specified in file F; if F is '-', then read names from standard input.
--exclude=PATTERN                      Exclude files that match PATTERN.
--max-depth=N                          Print the total for a directory (or file, with --all) only if it is N or fewer levels below the command line argument; --max-depth=0 is the same as --summarize.
--si                                   Like -h, but use powers of 1000 not 1024.
--time                                 Show time of the last modification of any file in the directory, or any of its subdirectories.
--time=WORD                            Show time as WORD instead of modification time: atime, access, use, ctime or status.
--time-style=STYLE                     Show times using STYLE, which can be full-iso, long-iso, iso, or +FORMAT; FORMAT is interpreted like in 'date'.
--help                                 Display this help and exit.
--version                              Output version information and exit.
```

### Examples

Sort files from largest to smallest:

```shell
ubuntu@VM-0-14-ubuntu:~/git-work/linux-command$ du -sh * |sort -rh
2.9M    command
1.9M    assets
148K    template
72K     package-lock.json
52K     dist
28K     build
16K     README.md
4.0K    renovate.json
4.0K    package.json
4.0K    LICENSE
```

Display only the size of subdirectories in the current directory:

```shell
ubuntu@VM-0-14-ubuntu:~/git-work/linux-command$ du -sh ./*/
1.9M    ./assets/
28K     ./build/
2.9M    ./command/
52K     ./dist/
148K    ./template/
```

Check the space occupied by files in a specified directory:

```shell
ubuntu@VM-0-14-ubuntu:~/git-work/linux-command/assets$ du ./*
144     ./alfred.png
452     ./chrome-extensions.gif
4       ./dash-icon.png
1312    ./Linux.gif
16      ./qr.png
```

Display only the total size:

```shell
ubuntu@VM-0-14-ubuntu:~/git-work/linux-command/assets$ du -s .
1932    .
```

Display the total size in a human-readable format:

```shell
ubuntu@VM-0-14-ubuntu:~/git-work/linux-command/assets$ du -sh .
1.9M    .
```
