dos2unix
===

Convert text files from DOS format to Unix format.

## Description

The **dos2unix** command is used to convert DOS-formatted text files to UNIX format (DOS/MAC to UNIX text file format converter). Text files in DOS use `\r\n` (CRLF) as a line break, which is `0D 0A` in hexadecimal. Unix text files use `\n` (LF) as a line break, which is `0A` in hexadecimal. When a DOS-formatted file is opened with an older version of `vi` in Linux, `^M` will appear at the end of each line, and many commands cannot handle this format correctly (e.g., shell scripts). Conversely, Unix-formatted files might appear as a single long line when opened in Windows Notepad. Therefore, there is a need to convert between these two formats. The corresponding tool to convert UNIX format to DOS is `unix2dos`.

### Syntax

```shell
dos2unix [-hkqV] [-c convmode] [-o file ...] [-n infile outfile ...]
```

### Options

```shell
-k    Keep the date stamp of the output file.
-q    Quiet mode, suppress all warnings.
-V    Display version information.
-c    Conversion mode. Modes: ASCII, 7bit, ISO, Mac. Default is ASCII.
-o    Write to the original file (overwrite).
-n    Write to a new file (specify input and output files).
```

### Parameters

File: The file(s) to be converted.

### Examples

The simplest usage is dos2unix followed by the filename:

```shell
dos2unix file
```

To convert multiple files at once, list them after the command (Note: you can use the `-o` parameter, but it is the same as the default behavior):

```shell
dos2unix file1 file2 file3
dos2unix -o file1 file2 file3
```

The above commands modify the original files. If you want to save the result to a new file while keeping the original file unchanged, use the `-n` parameter:

```shell
dos2unix -n oldfile newfile
```

To keep the file timestamp unchanged, add the `-k` parameter. This can be combined with other commands:

```shell
dos2unix -k file
dos2unix -k file1 file2 file3
dos2unix -k -o file1 file2 file3
dos2unix -k -n oldfile newfile
```

Convert all files in the current directory:

```shell
find . -type f | xargs dos2unix
```
