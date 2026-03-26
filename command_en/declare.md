declare
===

Declare variables and give them attributes.

## Syntax

```shell
declare [-aAfFgilnrtux] [-p] [name[=value] ...]
```

## Main Uses

- Display all variables and values with specified attributes.
- Display one or more variables and values with specified attributes.
- Display attributes and values of one or more variables.
- Display attributes and values of all variables and function definitions.
- Display attributes and values of all variables.
- Display attributes and values of all global variables.
- Display all function names and definitions.
- Display only all function names.
- Display one or more function names and definitions.
- Display only one or more function names.
- Declare global variables (optional: assignment).
- Declare variables (optional: assignment, attributes).
- Add or remove variable attributes (optional: assignment).

## Options

```shell
-f  Restrict action or display to function names and definitions.
-F  Restrict display to function names only (plus line number and source file when debugging).
-g  Create global variables when used in a shell function; ignored otherwise.
-p  Display attributes and values of each name.

*Attribute-setting options:
-a  To make NAMEs indexed arrays (if supported).
-A  To make NAMEs associative arrays (if supported).
-i  To make NAMEs have the 'integer' attribute.
+i  To remove the 'integer' attribute.
-l  To convert NAMEs to lower case on assignment.
+l  To remove the 'lower case' attribute.
-n  To make NAMEs reference variables (if supported).
+n  To remove the 'reference' attribute (if supported).
-r  To make NAMEs readonly.
-t  To make NAMEs have the 'trace' attribute.
+t  To remove the 'trace' attribute.
-u  To convert NAMEs to upper case on assignment.
+u  To remove the 'upper case' attribute.
-x  To mark NAMEs for export.
+x  To remove the 'export' attribute.
```

## Parameters

```shell
name (optional): Variable or function name.
value (optional): Value of the variable.
```

## Return Value

declare returns true unless an invalid option is supplied or an assignment error occurs.

## Examples

```shell
# Declare a variable.
declare reference_website='https://wangchujiang.com/linux-command/'

# Display all variables and values with the integer attribute.
declare -i
# Define variable b and assign 5, with integer attribute.
declare -i b=5
# Display attributes; returns: declare -i b="5".
declare -p b
# Remove integer attribute.
declare +i b
# Display attributes; returns: declare -- b="5".
declare -p b
# Force case conversion based on attributes.
declare -u uc_var='abc'
declare -l lc_var='ABC'
# Outputs 'ABC abc'
echo "${uc_var} ${lc_var}"
```

```shell
# Defining global variables inside a function.
function test(){
  declare -g a=3
  # Or
  local -g b=3
  # Or
  c=3
  # Check their attributes.
  declare -p a b c
}
# Execute the function.
test
# Result:
# declare -- a="3"
# declare -- b="3"
# declare -- c="3"

# Defining global variables outside a function.
declare a=3
b=3
declare -p a b
# Result:
# declare -- a="3"
# declare -- b="3"

# Defining local variables.
function test2(){
  local -i a=3
  declare -i b=3
}
test2
# Variables are gone (destroyed after function exits).
echo "${a} ${b}"
# Note that 'a=3' in a script usually declares a global variable.
```

```shell
# Note: You cannot use `+a` or `+A` to unset arrays, nor `+r` for readonly attributes.

# Define a readonly array and assign values.
declare -ar season=('Spring' 'Summer' 'Autumn' 'Winter')
# Or:
season=('Spring' 'Summer' 'Autumn' 'Winter')
declare -ar season
# Display all indexed arrays.
declare -a

# Define an associative array.
declare -A fruits=(['apple']='red' ['banana']='yellow')
# Display all associative arrays.
declare -A
```

```shell
# Display attributes/values of all variables and function definitions (long output).
declare
# Display attributes/values of all variables.
declare -p
# Display attributes/values of all global variables.
declare -g
```

```shell
# Display all function names and definitions.
declare -f
# Display only all function names.
declare -F

# Define two functions.
function func_a(){ echo $(date +"%F %T"); }
function func_b(){ cd /; ls -lh --sort=time; }
# Display names and definitions for specific functions.
declare -f func_a func_b
# Display only names, useful for verifying if a name is defined as a function.
declare -F func_a func_b
```

## Discussion

1. Global and Local Variables
   
   Understanding these concepts is crucial for script writing.
   
   - Global Variables: Persist throughout the script's execution unless explicitly deleted.
   - Local Variables: Defined within a function and deleted when the function exits.
   
   It is recommended to use `local` inside functions and `declare` outside functions.
   
   > *Avoid defining too many global variables in scripts to prevent unexpected side effects and debugging difficulties.*
   
2. Regarding `declare`, `typeset`, `export`, `local`, and `readonly` commands.
   
   These commands often provide clearer intent than generic `declare` options:
   - Use `export var` instead of `declare -x var` for exported variables.
   - Use `local` for variables within functions.
   - Use `readonly` for read-only variables.
   
   `typeset` is synonymous with `declare`.
   
3. Regarding Exceptions

   Various factors can cause `declare` to fail. For details, refer to the [Bash online documentation for declare](https://www.gnu.org/software/bash/manual/bash.html#index-declare) or run `info bash`.

### Notes

1. This is a Bash builtin command; use `help declare` for more information.
2. For more on the export attribute, see the `export` command.
3. For more on the readonly attribute, see the `readonly` command.
4. For more on the reference attribute, see the examples in the `unset` command documentation.
