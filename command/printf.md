printf
===

Format and print data.

## Table of Contents

- [Bash Builtin Command](#builtin-command)
- [External Command](#external-command)

## Builtin Command

#### Synopsis

```shell
printf [-v var] format [arguments]
```

#### Main Usage

- Formats arguments and prints them.

#### Options

```shell
-v var: Output the result to the variable var instead of standard output.
```

#### Parameters

format: Output format.

arguments: One or more arguments.

```shell
Escape Sequences: In addition to the escape sequences supported by printf(1) and printf(3), the builtin printf supports the following:

%b       Expand backslash escape characters in arguments.
%q       Quote arguments so they can be used as shell input.
%(fmt)T  Output date-time string according to strftime(3) escape characters.
```

#### Return Value

Returns success unless an invalid option is given, a write error occurs, or an assignment error occurs.

#### Examples

```shell
# %-5s: Formatted as a left-aligned string with a width of 5 ('-' denotes left alignment). Default is right-aligned.
# %-4.2f: Formatted as a left-aligned float with a width of 4 and 2 decimal places.

printf "%-5s %-10s %-4s\n" NO Name Mark
printf "%-5s %-10s %-4.2f\n" 01 Tom 90.3456
printf "%-5s %-10s %-4.2f\n" 02 Jack 89.2345
printf "%-5s %-10s %-4.2f\n" 03 Jeff 98.4323

# Output
NO    Name       Mark
01    Tom        90.35
02    Jack       89.23
03    Jeff       98.43


# Examples for %b %q %(fmt)T.
# Output with a newline.
printf "%s\n" 'hello world'
# Expand newline character, same result as above.
printf "%b" 'hello world\n'

printf '%q\n' 'a b c'
# Output
a\ b\ c

# %z is timezone, %n is newline.
printf "%( %F %T %z%n)T"
# Output
2019-09-10 01:48:07 +0000
```

#### Note

1. This command is a bash builtin; use the `help` command for related help information.


## External Command

#### Synopsis

```shell
printf FORMAT [ARGUMENT]...
printf OPTION
```

#### Main Usage

- Formats arguments and prints them.


#### Options

```shell
--help Display help information and exit.
--version Display version information and exit.
```

#### Parameters

format: Output format.

arguments: One or more arguments.

```shell
Note that (%b %q) are omitted here; if your coreutils version supports them, refer to the examples above.
Supported escape sequences:

\"          Double quote
\\          Backslash
\a          Alert (bell)
\b          Backspace
\c          Produce no further output
\e          Escape
\f          Form feed
\n          New line
\r          Carriage return
\t          Horizontal tab
\v          Vertical tab
\NNN        Octal number (1 to 3 digits)
\xHH        Hexadecimal number (1 to 2 digits)
\uHHHH      Unicode character with 4 hex digits
\UHHHHHHHH  Unicode character with 8 hex digits
%%          Literal %

And C format specifications ending in one of 'diouxXfeEgGcs', which will be converted to the correct type and handle variable widths.
```

#### Examples

```shell
# Use /usr/bin/printf to ensure the external command is called, not the builtin.
# You can use printf directly if the builtin is disabled or no such function exists.

# Print array indices and values line by line.

# Declaring an array doesn't strictly require 'declare -a' or 'local -a'.
arr=('line1' 'line2')
/usr/bin/printf "%s\n" ${!arr[@]}
# Output indices
0
1
/usr/bin/printf "%s\n" ${arr[@]}
# Output values
line1
line2

# Declaring an associative array (dictionary) must use 'declare -A' or 'local -A'.
declare -A assoc_arr=(['key1']='value1' ['key2']='value2')
/usr/bin/printf "%s\n" ${!assoc_arr[@]}
# Output keys.
key2
key1
/usr/bin/printf "%s\n" ${assoc_arr[@]}
# Output values.
value2
value1
```

#### Return Value

Returns success unless an invalid option is given, etc.

#### Note

1. This command is part of the `GNU coreutils` package; use `man 1 printf` or `info coreutils 'printf invocation'` for help.

2. To enable or disable builtin commands, use the `enable` command. For priority issues with same-named commands, see the `builtin` command examples.

3. Explanation of the format specifiers `%b %q %(fmt)T` from `bug-bash@gnu.org`:
   > The %b format specifier in printf(1) is a POSIX feature added beyond what printf(3) supports.
   >
   > The %q and %T specifiers are non-standard and not supported by all standalone printf implementations.
   
   More details can be found at:
   - [POSIX printf](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/printf.html) Section 5 of `APPLICATION USAGE`.
   - [POSIX printf Format Specifiers](https://pubs.opengroup.org/onlinepubs/9699919799/functions/printf.html) `Description` section.
