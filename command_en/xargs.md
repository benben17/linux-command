xargs
===

Build and execute command lines from standard input

## Description

The **xargs command** is a filter for passing arguments to other commands and a tool for combining multiple commands. It excels at converting standard input data into command-line arguments. `xargs` can process data from a pipe or stdin and convert it into arguments for a specific command. It can also reformat single-line or multi-line text input, such as converting multiple lines into a single line or vice versa. The default command for `xargs` is `echo`, and the default delimiter is whitespace. This means that input passed to `xargs` via a pipe will contain newlines and spaces, but through `xargs` processing, these will be replaced by spaces. `xargs` is a crucial component for building powerful one-liner commands.

### Basic Usage

`xargs` is often used as a formatting tool to read input data, reformat it, and output it.

Consider a test file `test.txt` with multi-line text:

```shell
cat test.txt

a b c d e f g
h i j k l m n
o p q
r s t
u v w x y z
```

Convert multi-line input to a single line:

```shell
cat test.txt | xargs

a b c d e f g h i j k l m n o p q r s t u v w x y z
```

#### Multi-line output with -n
The **-n option** specifies the maximum number of arguments per command line:

```shell
cat test.txt | xargs -n3

a b c
d e f
g h i
j k l
m n o
p q r
s t u
v w x
y z
```

#### Custom delimiter with -d
The **-d option** allows you to define a custom delimiter:

```shell
echo "nameXnameXnameXname" | xargs -dX

name name name name
```

Combined with the **-n option**:

```shell
echo "nameXnameXnameXname" | xargs -dX -n2

name name
name name
```

#### Reading from stdin
**Read from stdin and pass formatted arguments to a command**

Assume a script `sk.sh` and a file `arg.txt` containing arguments:

```shell
#!/bin/bash
# sk.sh content: print all arguments
echo $*
```

`arg.txt` content:

```shell
cat arg.txt

aaa
bbb
ccc
```

#### Using the -I option
The **-I option** specifies a replacement string (e.g., `{}`). This string will be replaced by the actual argument when `xargs` expands the command. When used with `xargs`, the command is executed once for each argument:

```shell
cat arg.txt | xargs -I {} ./sk.sh -p {} -l

-p aaa -l
-p bbb -l
-p ccc -l
```

Copy all image files to the `/data/images` directory:

```shell
ls *.jpg | xargs -n1 -I{} cp {} /data/images
```

#### Combined with the find command
**Using xargs with find**

When deleting too many files with `rm`, you might encounter the error: `/bin/rm: Argument list too long`. Use `xargs` to avoid this:

```shell
find . -type f -name "*.log" -print0 | xargs -0 rm -f
```

The `-0` option tells `xargs` to use the null character (`\0`) as a delimiter.

Count the total lines of all `.php` files in a source code directory:

```shell
find . -type f -name "*.php" -print0 | xargs -0 wc -l
```

Find all `.jpg` files and compress them into an archive:

```shell
find . -type f -name "*.jpg" -print | xargs tar -czvf images.tar.gz
```

#### Print the command being executed
Use the `-t` option to print the command before executing it:

```shell
ls | xargs -t -I{} echo {}
```

This will display the file list and the corresponding `echo` commands being run.

#### Confirm execution with -p
The `-p` option prompts for confirmation before running each command. Use this when you need to be very precise:

```shell
find . -maxdepth 1 -name "*.log" | xargs -p -I{} rm {}
```

#### Execute multiple commands
Use the `-I` option to let `xargs` run multiple commands (via `sh -c`):

```shell
cat foo.txt | xargs -I % sh -c 'echo %; mkdir %'
```

#### Other Applications
If you have a file containing many URLs you want to download:

```shell
cat url-list.txt | xargs wget -c
```

### Subshells

When running a shell script, another command interpreter is started, similar to how commands are interpreted at the command prompt. Each shell script effectively runs in a child process of the parent shell.

```shell
cmd1 | ( cmd2; cmd3; cmd4 ) | cmd5
```

If `cmd2` is `cd /`, it only changes the working directory within the subshell. `cmd5` remains unaffected by this change. Commands within parentheses `()` are executed in a subshell, and variables defined there are local to that subshell.

Subshells can be used to set temporary environment variables for a group of commands:

```shell
COMMAND1
COMMAND2
(
  IFS=:
  PATH=/bin
  unset TERMINFO
  COMMAND4
  COMMAND5
  exit 3 # Exits only from the subshell
)
COMMAND6
```

## References

- [Unix xargs command](https://shapeshed.com/unix-xargs/)
