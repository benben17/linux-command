help
===

Display help information for bash built-in commands.

## Supplemental Information

The **help command** is a bash built-in that displays information for other shell built-in commands. To view help for external commands, use `man` or `info`.

### Syntax

```shell
help [options] [pattern ...]
```

### Options

```shell
-d: Display a short description for each pattern.
-m: Display usage in a format similar to a man page.
-s: Display only a short usage synopsis for each pattern.
If no options are specified: Displays help information similar to -m but without specific sections like 'SEE ALSO' or 'IMPLEMENTATION'.
```

### Parameters

bash built-in commands (one or more, separated by spaces).

### Frequently Asked Questions

Q: Which commands are bash built-ins? How can I tell if a command is a built-in?
A: You can use `man builtin` or `man builtins`. You can also check the help for the bash built-in command `type`.

Q: How can I get help for the `help` command itself?
A: Pass `help` as an argument to the `help` command: `help help`.

Q: Why can I also use `man echo` to see help for `echo`?
A: Because besides the bash built-in `echo`, there is also an `echo` command in the GNU/Linux `coreutils` package. The `man` page for `echo` usually contains a note about the differences between the built-in and the standalone version.

PS: If you define a function named `echo` in a shell script, what is the execution priority?
Refer to the `builtin` command.

Q: I need more help with bash.
A: You can run `man bash`, `info bash`, visit the [official bash website](http://www.gnu.org/software/bash/), or use search engines.

### Examples

Display help information for the shell's internal `shopt` command:

```shell
help shopt
shopt: shopt [-pqsu] [-o long-option] optname [optname...]
    Toggle the values of variables controlling optional behavior.
    The -s flag means to enable (set) each OPTNAME; the -u flag
    unsets each OPTNAME.  The -q flag suppresses output; the exit
    status indicates whether each OPTNAME is set or unset.  The -o
    option restricts the OPTNAMEs to those defined for use with
    `set -o'.  With no options, or with the -p option, a list of all
    settable options is displayed, with an indication of whether or
    not each is set.
```
