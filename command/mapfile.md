mapfile
===

Read lines from standard input into an array variable

## Overview

```shell
mapfile [-d delim] [-n count] [-O origin] [-s count] [-t] [-u fd] [-C callback] [-c quantum] [array]
```

## Description

The **mapfile** (or **readarray**) command reads lines from standard input or a file descriptor and assigns them to an indexed array variable.

## Options

```shell
-d delim       Use 'delim' as the line terminator instead of the default newline.
-n count       Read at most 'count' lines. If 'count' is 0, all lines are read.
-O origin      Begin assigning to the array at index 'origin'. Default is 0.
-s count       Discard the first 'count' lines read.
-t             Remove the trailing delimiter (default newline) from each line.
-u fd          Read from file descriptor 'fd' instead of standard input.
-C callback    Evaluate 'callback' each time 'quantum' lines are read.
-c quantum     Specify the number of lines read between each call to 'callback'.

If -C is used without -c, the default quantum is 5000.
When the callback is executed, it is passed the index of the next array element to be assigned and the line just read as additional arguments.
If -O is not specified, mapfile clears the target array before assignment.
```

### Parameters

array (optional): The name of the array variable. If not provided, the default name `MAPFILE` is used.

## Return Value

Returns success unless an invalid option is provided, the array is read-only, or the array is not an indexed array.

## Examples

```shell
# Common usage
mapfile < source_file target_array
cat source_file | mapfile target_array
mapfile -u fd target_array

# Read only the first 5 lines
mapfile < source_file -n 5 target_array

# Skip the first 5 lines
mapfile < source_file -s 5 target_array

# Assign starting from index 2
mapfile < source_file -O 2 target_array

# Use tab as the delimiter
mapfile < source_file -d $'\t' target_array

# Remove the delimiter (tab) while reading
mapfile < source_file -d $'\t' -t target_array
# Remove the delimiter (newline) while reading
mapfile < source_file -t target_array

# Execute a callback every 2 lines
mapfile < source_file -C "echo CALLBACK:" -c 2 target_array

# Iterate through the array and print elements
for i in ${!target_array[@]}; do
  printf "%s" ${target_array[i]}
done
```

### Notes

1. This is a Bash built-in command. Use `help mapfile` for more information.
2. `readarray` is a synonym for `mapfile`.
