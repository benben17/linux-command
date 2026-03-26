# read

Read variable values from standard input (keyboard).

## Description

The **read** command reads values from standard input and assigns them to variables. It is commonly used in shell scripts for user interaction. This command can read values for multiple variables at once; both the variables and the input values should be separated by spaces. If no variable name is specified, the input is automatically assigned to the built-in variable `REPLY`.

### Syntax

```shell
read [options] [parameters]
```

### Options

```shell
-a array: Assign the words read to sequential indices of the array variable `array`.
-d delim: Continue reading until the first character of `delim` is read, rather than newline.
-n nchars: Return after reading `nchars` characters rather than waiting for a complete line of input.
-p prompt: Display the string `prompt` without a trailing newline before attempting to read.
-r: Raw mode; do not treat backslashes as escape characters.
-s: Silent mode; characters read from a terminal are not echoed (useful for passwords).
-t timeout: Terminate and return failure if a complete line of input is not read within `timeout` seconds.
```

### Parameters

Variable: Specifies the name of the variable to store the input value.

### Examples

**Common usage of the read command:**

```shell
read myvar
# Read from standard input and assign to variable 'myvar'.
```

```shell
read first last
# Read input until the first space or newline; put the first word into 'first', and the rest of the line into 'last'.
```

```shell
read
# Read a line from standard input and assign to the built-in variable 'REPLY'.
```

```shell
read -a friends
# Read a list of words into the array 'friends'.
```

```shell
read -p "Enter your name: " name
# Display a prompt, wait for input, and store the result in 'name'.
```

```shell
read -r line
# Allow the input to contain backslashes literally.
```

```shell
read -t 3
# Wait for input for a maximum of 3 seconds.
```

```shell
read -n 2 var
# Read exactly two characters into 'var' without needing to press Enter.
```

```shell
read -d ":" var
# End the input when the character ':' is typed.
```

---

**Detailed Examples:**

**Reading into multiple variables:**

```shell
# read one two three
1 2 3                   # Console input: 1 2 3 (separated by spaces)

# echo "one = $one, two = $two, three = $three"
one = 1, two = 2, three = 3
```

**Using the REPLY variable:**

```shell
# read                  # Wait for input
This is REPLY           # Input provided

# echo $REPLY
This is REPLY
```

**Using the -p prompt option:**

```shell
# read -p "Enter your name: "
Enter your name: stephen                 # Input 'stephen' after the prompt

# echo $REPLY
stephen
```

**Reading into an array:**

```shell
# read -a friends
Tim Tom Helen

# echo "They are ${friends[0]}, ${friends[1]} and ${friends[2]}."
They are Tim, Tom and Helen.
```

**Masking password input:**

Method 1: Using the `-s` (silent) option.

```shell
#!/bin/bash
read -p "Enter password: " -s pwd
echo
echo "Password read successfully."
```

Method 2: Using `stty` to disable echoing.

```shell
#!/bin/bash
stty -echo
read -p "Enter password: " pwd
stty echo
echo
echo "Input complete."
```

The `stty -echo` command disables echoing of characters to the terminal, while `stty echo` re-enables it.

**Basic assignment and verification:**

```shell
read v1 v2          # Read two variables
# User enters: Linux Bash

echo $v1 $v2        # Output: Linux Bash
```

*Note: When using `echo` to output variable values, you must prefix the variable name with the `$` symbol; otherwise, `echo` will just print the name of the variable itself.*
