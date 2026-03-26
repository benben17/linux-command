true
===

Return a successful exit status.

## Synopsis

```shell
true
```

## Main Purpose

- Used for logical operations with other commands.

## Return Value

Always returns a successful status; the return value is 0.

## Example

```shell
# When your script is set to 'set -e', any command returning failure will cause the script to exit.
set -e
# How to temporarily skip this? The following statement uses the logical OR operator with true, ensuring the return value is always true.
some_command || true

# Similarly to 'pass' in Python, it can also be used as a placeholder in conditional statements.
```

### Notes

1. This command is a bash built-in; see the `help` command for related help information.
