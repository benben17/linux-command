exit
===

Exit the current shell.

## Synopsis

```shell
exit [n]
```

## Description

- Executing `exit` causes the shell to terminate with the specified exit status `n`.
- If `n` is omitted, the exit status is that of the last command executed.

## Parameters

n (optional): The specified shell return value (an integer).

## Return Value

Returns the value specified by `n`. If `n` is greater than 255 or less than 0, the value is normalized to the range 0 to 255 (e.g., by adding or subtracting 256).

## Examples

Exit the current shell:

```shell
[root@localhost ~]# exit
logout
```

You can also use `Ctrl+D` to exit the terminal. Here is how to enable or disable this feature:

```shell
# Enable Ctrl+D to exit terminal
set +o ignoreeof
# Disable Ctrl+D to exit terminal
set -o ignoreeof
```

In a script, enter the script's directory or exit:

```shell
cd $(dirname $0) || exit 1
```

In a script, check the number of arguments; exit if it doesn't match:

```shell
if [ "$#" -ne "2" ]; then
    echo "usage: $0 <area> <hours>"
    exit 2
fi
```

In a script, delete temporary files upon exiting:

```shell
trap "rm -f tmpfile; echo Bye." EXIT
```

Check the exit code of the previous command:

```shell
./mycommand.sh
EXCODE=$?
if [ "$EXCODE" == "0" ]; then
    echo "O.K"
fi
```

### Note

1. This is a bash built-in command. For more help, use the `help` command.
