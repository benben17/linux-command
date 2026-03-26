continue
===

Ends the current iteration of a loop and continues with the next iteration of a `for`, `while`, or `until` loop.

## Synopsis

```shell
continue [n]
```

## Main Purpose

- Ends the current iteration of the loop and starts the next one; can specify which nested level to continue from.

## Arguments

n (optional): An integer greater than or equal to 1, specifying the nested level of the loop to continue.

## Return Value

Returns success unless `n` is less than 1.

## Examples

```shell
# The default value of the optional parameter n is 1.
for((i=3;i>0;i--)); do
  # Skip to the next iteration of the inner for loop.
  for((j=3;j>0;j--)); do
    if((j==2)); then
      # continue 1 produces the same result.
      continue
    fi
  printf "%s %s\n" ${i} ${j}
  done
done
# Output
3 3
3 1
2 3
2 1
1 3
1 1
```

```shell
# When n is 2:
# Skip to the next iteration of the outer for loop.
for((i=3;i>0;i--)); do
  for((j=3;j>0;j--)); do
    if((j==2)); then
      continue 2
    fi
  printf "%s %s\n" ${i} ${j}
  done
done
# Output
3 3
2 3
1 3
```

### Note

1. This is a bash built-in command. For more help, use the `help` command.
观察
