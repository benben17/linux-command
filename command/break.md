break
===

Exit from for, while, or until loops.

## Synopsis

```shell
break [n]
```

## Main Purpose

- Exit from for, while, or until loops, optionally specifying the number of nested levels to break out of.

## Parameters

n (optional): An integer greater than or equal to 1, used to specify the number of nested loop levels to exit.

## Return Value

Returns success unless `n` is less than 1.

## Examples

```shell
# The default value for the optional parameter n is 1.
# Continues execution from the outer for loop.
for ((i=3; i>0; i--)); do
  for ((j=3; j>0; j--)); do
    if ((j==2)); then
      # The result is the same as break 1
      break
    fi
    printf "%s %s\n" ${i} ${j}
  done
done
# Output results
3 3
2 3
1 3
```

```shell
# When n is 2:
# Exits two levels of loops and finishes.
for ((i=3; i>0; i--)); do
  for ((j=3; j>0; j--)); do
    if ((j==2)); then
      break 2
    fi
    printf "%s %s\n" ${i} ${j}
  done
done
# Output results
3 3
```

### Notes

1. This command is a bash built-in; for related help information, please use the `help` command.
