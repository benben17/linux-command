cd
===

Change the shell working directory.

## Synopsis

```shell
cd [-L|[-P [-e]]] [dir]
```

## Main Purpose

- Change the current working directory to `dir`. The `dir` can be an absolute or relative path.
- If the `dir` argument is omitted, it defaults to the value of the `HOME` shell variable.
- If `dir` is specified as `~`, it represents the user's `HOME` directory; `.` represents the current directory, and `..` represents the parent directory.
- The `CDPATH` environment variable is a colon-separated list of directories. You can add the parent directories of frequently visited locations to `CDPATH` for easier access; if `dir` starts with `/`, `CDPATH` is not used.
- When the `shopt` option `cdable_vars` is enabled, if `dir` does not exist in `CDPATH` or the current directory, it will be treated as a variable, and its value will be used as the destination directory.

## Parameters

dir (optional): Specify the directory to switch to.

## Options

```shell
-L (default) If the target directory is a symbolic link, follow the link.
-P If the target directory is a symbolic link, use the physical directory structure instead of following symbolic links.
-  Switch the current working directory to the directory represented by the OLDPWD environment variable, which is the previous working directory.
```

## Return Value

Returns success unless the specified directory cannot be entered.

## Examples

```shell
cd    # Enter the user's home directory.
cd /  # Enter the root directory.
cd ~  # Enter the user's home directory.
cd ..  # Return to the parent directory (if the current directory is "/", it remains at "/").
cd ../..  # Return two levels up.
cd !$  # Use the argument of the last command as the argument for cd.
```

Note on switching to the previous working directory:

```shell
cd -
# This command first displays the target directory before entering it.
cd ${OLDPWD}
# This command switches directly to the previous working directory.
```

About `CDPATH`:

```shell
# Set the Desktop folder as the value for CDPATH.
CDPATH='~/Desktop'
# Assume there is no test3 folder in ~ or ~/Desktop for this demonstration; create them now.
mkdir ~/test3
mkdir ~/Desktop/test3
# Enter the ~ directory.
cd ~
# Enter the test3 directory.
cd test3
# After execution, ~/Desktop/test3 is displayed and entered, rather than the test3 directory under ~.
# If CDPATH has a value, it prioritizes searching CDPATH and enters the first successful match. If all fail, it finally tries the current directory.
```

About `cdable_vars`:

```shell
# Enable the option.
shopt -s cdable_vars
# Assume there is no directory named new_var in the current path or CDPATH.
new_var='~/Desktop'
# Attempt to enter.
cd new_var
# Disable the option.
shopt -u cdable_vars
```

### Notes

1. This command is a bash built-in; for related help information, please use the `help` command.
2. It is recommended to add necessary comments when using the `cd` command in scripts to remind readers of the current working directory and avoid issues like "file not found."
