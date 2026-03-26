export
===

Set the export attribute for shell variables or functions.

## Synopsis

```
export [-fn] [name[=word]]...
export -p
```

## Description

- Define one or more variables and set the export attribute.
- Modify the value of one or more variables and set the export attribute.
- Remove the export attribute from one or more variables.
- Display all variables that have the export attribute.
- Add the export attribute to one or more defined functions.
- Remove the export attribute from one or more functions.
- Display all functions that have the export attribute.

## Options

```shell
-f: Refers to functions.
-n: Remove the export attribute from variables.
-p: Display all variables with the export attribute.
-pf: Display all functions with the export attribute.
-nf: Remove the export attribute from functions.
--: Subsequent options are ignored.
```

## Parameters

name (optional): Variable name or defined function name.

value (optional): The value of the variable.

### Return Value

`export` returns true unless an invalid option or name is provided.

## Examples

```shell
# Display all exported variables
# export -p
# export
# Display all exported functions
# export -pf
```

```shell
# Delete demo variables first
# unset a b
# Define variables and export them
export a b=3
# Or define first and export later
b=3
export b

# Modify values of exported variables
export a=5 b=7
# Or assign values directly
a=5; b=7

# Remove export attribute from variables
export -n a b
```

```shell
# Delete demo functions first
unset func_1 func_2
# Create functions
function func_1(){ echo '123'; }
function func_2(){ echo '890'; }

# Export defined functions
export -f func_1 func_2

# Remove export attribute from functions
export -fn func_1 func_2
```

```shell
# Add environment variable (JAVA) to `~/.bashrc`
export PATH=/usr/local/jdk1.7.0/bin:$PATH
# Add current path to dynamic library path
export LD_LIBRARY_PATH=$(pwd):${LD_LIBRARY_PATH}
```

## Common Errors

- Adding the export attribute to an undefined function.
- Removing the export attribute from a function/variable that is not exported.
- Using options after `--`.

## Q&A

#### Q: What is the purpose of setting the export attribute for variables or functions?

A: They become environment variables that can be accessed by child processes spawned by the current shell.

#### Q: If my script modifies an existing environment variable, will it take effect in the current terminal? Will it affect previously or subsequently opened terminals?

A: Only scripts executed via the `source` (or `.`) command will affect the current shell. Otherwise, the script runs in a sub-shell and its changes are lost when it exits. Previously opened terminals are not affected. Subsequently opened terminals are only affected if you modified a startup script like `~/.bashrc`.

#### Q: I have a script that calls functions and variables defined in `~/.bashrc`. Why can't I use them when I run the script via `sh` or as an executable?

A: Ensure that you have `export`ed them in `~/.bashrc`.

#### Q: Can arrays and associative arrays be exported?

A: Yes (if your bash version supports them), but there are some known issues and limitations.

#### Q: Why does the output start with `declare` when I view exported attributes?

A: Because `declare` can also set export attributes for variables or functions. See the `declare` command for details.

### Note

1. This is a bash built-in command. For more help, use the `help` command.

### Knowledge Points

In `info bash` or the [Bash Online Manual](http://www.gnu.org/software/bash/manual/bash.html), section `3.7.3` (Shell Execution Environment) mentions:

> - shell parameters that are set by variable assignment or with set or inherited from the shell’s parent in the environment
> - shell functions defined during execution or inherited from the shell’s parent in the environment

A variable is a parameter denoted by a name. Sub-shells inherit exported variables and functions from the parent shell.

### Further Reading

Setting environment variables is common when configuring cross-compilation toolchains. To view existing environment variables:

```shell
[root@localhost ~]# export
declare -x G_BROKEN_FILENAMES="1"
declare -x HISTSIZE="1000"
declare -x HOME="/root"
declare -x hostname="localhost"
declare -x INPUTRC="/etc/inputrc"
declare -x LANG="en_US.UTF-8"
declare -x LESSOPEN="|/usr/bin/lesspipe.sh %s"
declare -x logname="root"
declare -x LS_COLORS="no=00:fi=00:di=01;34:ln=01;36:pi=40;33:so=01;35:bd=40;33;01:cd=40;33;01:or=01;05;37;41:mi=01;05;37;41:ex=01;32:*.cmd=01;32:*.exe=01;32:*.com=01;32:*.btm=01;32:*.bat=01;32:*.sh=01;32:*.csh=01;32:*.tar=01;31:*.tgz=01;31:*.arj=01;31:*.taz=01;31:*.lzh=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.gz=01;31:*.bz2=01;31:*.bz=01;31:*.tz=01;31:*.rpm=01;31:*.cpio=01;31:*.jpg=01;35:*.gif=01;35:*.bmp=01;35:*.xbm=01;35:*.xpm=01;35:*.png=01;35:*.tif=01;35:"
declare -x mail="/var/spool/mail/root"
declare -x OLDPWD
declare -x PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
declare -x pwd="/root"
declare -x SHELL="/bin/bash"
declare -x SHLVL="1"
declare -x SSH_CLIENT="192.168.2.111 2705 22"
declare -x SSH_CONNECTION="192.168.2.111 2705 192.168.2.2 22"
declare -x SSH_TTY="/dev/pts/0"
declare -x TERM="linux"
declare -x USER="root"
```
