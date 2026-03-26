awk
===

A programming language for processing text and data

## Additional Information

**awk** is a programming language used for processing text and data under Linux/Unix. Data can come from standard input (stdin), one or more files, or the output of other commands. It supports advanced features such as user-defined functions and dynamic regular expressions, making it a powerful programming tool for Linux/Unix. It is used on the command line but even more frequently as a script. awk has many built-in features, such as arrays and functions, which it shares with the C language. Its flexibility is its greatest advantage.

## awk Command Format and Options

**Syntax**

```shell
awk [options] 'script' var=value file(s)
awk [options] -f scriptfile var=value file(s)
```

**Common Command Options**

* **-F fs**: Specifies the input field separator. `fs` can be a string or a regular expression, such as `-F:`. The default separator is consecutive spaces or tabs.
* **-v var=value**: Assigns a value to a user-defined variable, passing external variables to awk.
* **-f scriptfile**: Reads awk commands from a script file.
* **-m[fr] val**: Sets internal limits on `val`. The `-mf` option limits the maximum number of blocks allocated to `val`; the `-mr` option limits the maximum number of records. These two features are extensions from the Bell Labs version of awk and are not applicable in standard awk.

## awk Patterns and Actions

An awk script consists of patterns and actions.

### Pattern

A pattern can be any of the following:

* `/regular expression/`: Uses an extended set of wildcards.
* Relational expression: Uses operators for operations, which can be string or numeric comparison tests.
* Pattern matching expression: Uses operators `~` (match) and `!~` (no match).
* BEGIN block, pattern block, END block: See "How awk works".

### Action

An action consists of one or more commands, functions, or expressions separated by newlines or semicolons and enclosed in curly braces. Key components include:

* Variable or array assignment
* Output commands
* Built-in functions
* Control flow statements

## Basic Structure of an awk Script

```shell
awk 'BEGIN{ print "start" } pattern{ commands } END{ print "end" }' file
```

An awk script typically consists of three parts: a BEGIN block, a general block that can use pattern matching, and an END block. These three parts are optional. Any part can be omitted from the script. The script is usually enclosed in **single quotes**, for example:

```shell
awk 'BEGIN{ i=0 } { i++ } END{ print i }' filename
```

### How awk works

```shell
awk 'BEGIN{ commands } pattern{ commands } END{ commands }'
```

* **Step 1**: Execute the statements in the `BEGIN{ commands }` block.
* **Step 2**: Read a line from the file or standard input (stdin), then execute the `pattern{ commands }` block. It scans the file line by line, repeating this process from the first line to the last until the entire file has been read.
* **Step 3**: When the end of the input stream is reached, execute the `END{ commands }` block.

The **BEGIN block** is executed **before** awk begins reading lines from the input stream. This is an optional block; statements such as variable initialization and printing table headers are typically written here.

The **END block** is executed **after** awk has finished reading all lines from the input stream. Tasks such as printing analysis results of all lines or information summaries are completed in the END block. It is also an optional block.

The general commands in the **pattern block** are the most important part and are also optional. If no pattern block is provided, `{ print }` is executed by default, which prints every line read. This block is executed for every line read by awk.

**Example**

```shell
echo -e "A line 1\nA line 2" | awk 'BEGIN{ print "Start" } { print } END{ print "End" }'
Start
A line 1
A line 2
End
```

When `print` is used without parameters, it prints the current line. When parameters for `print` are separated by commas, they are printed with a space as the delimiter. In awk's print block, double quotes are used as concatenation operators, for example:

```shell
echo | awk '{ var1="v1"; var2="v2"; var3="v3"; print var1,var2,var3; }' 
v1 v2 v3
```

Concatenation using double quotes:

```shell
echo | awk '{ var1="v1"; var2="v2"; var3="v3"; print var1"="var2"="var3; }'
v1=v2=v3
```

`{ }` acts like a loop body that iterates over every line in the file. Typically, variable initialization statements (e.g., `i=0`) and statements for printing the file header are placed in the BEGIN block, while statements for printing results are placed in the END block.

## awk Built-in Variables (Predefined Variables)

Note: [A][N][P][G] indicates the first tool to support the variable: [A]=awk, [N]=nawk, [P]=POSIX awk, [G]=gawk.

```shell
 **$n**  The nth field of the current record. For example, n=1 represents the first field, n=2 represents the second field. 
 **$0**  This variable contains the text content of the current line during execution.
[N]  **ARGC**  Number of command-line arguments.
[G]  **ARGIND**  Position of the current file in the command line (starting from 0).
[N]  **ARGV**  Array containing command-line arguments.
[G]  **CONVFMT**  Number conversion format (default value is %.6g).
[P]  **ENVIRON**  Associative array of environment variables.
[N]  **ERRNO**  Description of the last system error.
[G]  **FIELDWIDTHS**  List of field widths (separated by spaces).
[A]  **FILENAME**  Name of the current input file.
[P]  **FNR**  Similar to NR, but relative to the current file.
[A]  **FS**  Field separator (default is any whitespace).
[G]  **IGNORECASE**  If true, performs case-insensitive matching.
[A]  **NF**  Number of fields in the current record during execution.
[A]  **NR**  Number of records (line number) during execution.
[A]  **OFMT**  Output format for numbers (default value is %.6g).
[A]  **OFS**  Output field separator (default value is a space).
[A]  **ORS**  Output record separator (default value is a newline).
[A]  **RS**  Record separator (default value is a newline).
[N]  **RSTART**  First position of the string matched by the match function.
[N]  **RLENGTH**  Length of the string matched by the match function.
[N]  **SUBSEP**  Array subscript separator (default value is \034).
```

Escape Sequences

```
\\ \ itself
\$ Escaped $
\t Tab
\b Backspace
\r Carriage return
\n Newline
\c Cancel newline
```

**Example**

```shell
echo -e "line1 f2 f3\nline2 f4 f5\nline3 f6 f7" | awk '{print "Line No:"NR", No of fields:"NF, "$0="$0, "$1="$1, "$2="$2, "$3="$3}' 
Line No:1, No of fields:3 $0=line1 f2 f3 $1=line1 $2=f2 $3=f3
Line No:2, No of fields:3 $0=line2 f4 f5 $1=line2 $2=f4 $3=f5
Line No:3, No of fields:3 $0=line3 f6 f7 $1=line3 $2=f6 $3=f7
```

Use `print $NF` to print the last field in a line, `$(NF-1)` to print the second to last field, and so on:

```shell
echo -e "line1 f2 f3\n line2 f4 f5" | awk '{print $NF}'
f3
f5
```

```shell
echo -e "line1 f2 f3\n line2 f4 f5" | awk '{print $(NF-1)}'
f2
f4
```

Print the second and third fields of every line:

```shell
awk '{ print $2,$3 }' filename
```

Count the number of lines in a file:

```shell
awk 'END{ print NR }' filename
```

The above command uses only the END block. As each line is read, awk updates `NR` to the corresponding line number. When the last line is reached, the value of `NR` is the total number of lines, so `NR` in the END block represents the line count of the file.

An example of summing the values of the first field in every line:

```shell
seq 5 | awk 'BEGIN{ sum=0; print "Total sum:" } { print $1"+"; sum+=$1 } END{ print "equals"; print sum }' 
Total sum:
1+
2+
3+
4+
5+
equals
15
```

## Passing External Variables to awk

With the **`-v` option**, you can pass external values (not from stdin) to awk:

```shell
VAR=10000
echo | awk -v VARIABLE=$VAR '{ print VARIABLE }'
```

Another method to pass external variables:

```shell
var1="aaa"
var2="bbb"
echo | awk '{ print v1,v2 }' v1=$var1 v2=$var2
```

When input comes from a file:

```shell
awk '{ print v1,v2 }' v1=$var1 v2=$var2 filename
```

In the above method, variables are separated by spaces as command-line arguments to awk, following the BEGIN, {}, and END blocks.

## Finding Process PID

```shell
netstat -antup | grep 7770 | awk '{ print $NF NR}' | awk '{ print $1}'
```

## awk Operations and Logic

As a feature of a programming language, awk supports multiple operations, which are essentially the same as those in C. awk also provides a series of built-in arithmetic functions (such as `log`, `sqrt`, `cos`, `sin`, etc.) and string functions (such as `length`, `substr`, etc.). Referencing these functions greatly enhances awk's computing capabilities. Relational judgment is a standard feature in every programming language, and awk is no exception. awk allows for various tests, including pattern matching expressions `~` (match) and `!~` (no match). As an extension to testing, awk also supports logical operators.

### Arithmetic Operators

| Operator | Description |
| ----- | ---- |
| + - | Addition, Subtraction |
| * / % | Multiplication, Division, and Modulo |
| + - ! | Unary plus, minus, and logical NOT |
| ^ ** | Exponentiation |
| ++ -- | Increment or Decrement, as prefix or suffix |

Example:

```shell
awk 'BEGIN{a="b";print a++,++a;}'
0 2
```

Note: All arithmetic operations automatically convert operands to numeric values; non-numeric values become 0.

### Assignment Operators

| Operator | Description |
| ----- | ---- |
| = += -= *= /= %= ^= **= | Assignment statements |

Example:

```shell
a+=5; is equivalent to: a=a+5; and so on for others.
```

### Logical Operators

| Operator | Description |
| ----- | ---- |
| `||` | Logical OR |
| && | Logical AND |

Example:

```shell
awk 'BEGIN{a=1;b=2;print (a>5 && b<=2),(a>5 || b<=2);}'
0 1
```

### Regular Expression Operators

| Operator | Description |
| ----- | ---- |
| ~ !~ | Match regular expression and Do not match regular expression |

```
^ Beginning of line
$ End of line
. Any single character except newline
* Zero or more of the preceding character
.* All characters
[] Any one character in the character set
[^] Negate each character in the character set (does not match any character in the set)
^[^] Lines starting with characters not in the set
[a-z] Lowercase letters
[A-Z] Uppercase letters
[a-Z] Lowercase and uppercase letters
[0-9] Numbers
\< Beginning of word (words are generally separated by spaces or special characters; consecutive strings are treated as words)
\> End of word
```

> Regular expressions need to be enclosed in `/regex/`.

Example:

```shell
awk 'BEGIN{a="100testa";if(a ~ /^100*/){print "ok";}}'
ok
```

### Relational Operators

| Operator | Description |
| ----- | ---- |
| < <= > >= != == | Relational operators |

Example:

```shell
awk 'BEGIN{a=11;if(a >= 9){print "ok";}}'
ok
```

Note: `>` and `<` can be used for string comparison as well as numeric comparison. If operands are strings, they will be compared as strings. Numeric comparison occurs only if both are numbers. String comparison follows ASCII order.

### Other Operators

| Operator | Description |
| ----- | ---- |
| $ | Field reference |
| (space) | String concatenation |
| ?: | C-style conditional expression |
| in | Whether a key exists in an array |

Example:

```shell
awk 'BEGIN{a="b";print a=="b"?"ok":"err";}'
ok
```

```shell
awk 'BEGIN{a="b";arr[0]="b";arr[1]="c";print (a in arr);}'
0
```

```shell
awk 'BEGIN{a="b";arr[0]="b";arr["b"]="c";print (a in arr);}'
1
```

### Operator Precedence Table

Higher level indicates higher precedence.

## Advanced I/O in awk

### Reading the Next Record

Use of the `next` statement in awk: During line-by-line matching, if `next` is encountered, the current line is skipped, the following statements are ignored, and matching for the next line begins. The `next` statement is commonly used for merging multiple lines:

```shell
cat text.txt
a
b
c
d
e

awk 'NR%2==1{next}{print NR,$0;}' text.txt
2 b
4 d
```

When the remainder of the line number divided by 2 is 1, skip the current line. The following `print NR,$0` will not be executed. Starting from the next line, the program re-evaluates `NR%2`. Since the line number is 2, the statement block `{print NR,$0}` will be executed.

Skip lines starting with "web", and then merge the content of those lines with the following lines that do not start with "web", connecting them with a ":" and a tab:

```shell
cat text.txt
web01[192.168.2.100]
httpd            ok
tomcat               ok
sendmail               ok
web02[192.168.2.101]
httpd            ok
postfix               ok
web03[192.168.2.102]
mysqld            ok
httpd               ok

awk '/^web/{T=$0;next;}{print T":\t"$0;}' text.txt
web01[192.168.2.100]:   httpd            ok
web01[192.168.2.100]:   tomcat               ok
web01[192.168.2.100]:   sendmail               ok
web02[192.168.2.101]:   httpd            ok
web02[192.168.2.101]:   postfix               ok
web03[192.168.2.102]:   mysqld            ok
web03[192.168.2.102]:   httpd               ok
```

### Reading a Record Simply

Use of `awk getline`: Output redirection requires the `getline` function. `getline` obtains input from standard input, pipes, or input files other than the one currently being processed. it is responsible for obtaining the next line from the input and assigning values to built-in variables like `NF`, `NR`, and `FNR`. If a record is obtained, the `getline` function returns 1; if it reaches the end of the file, it returns 0; if an error occurs (such as failing to open a file), it returns -1.

`getline` syntax: `getline var`, where the variable `var` contains the content of a specific line.

Overall usage of `awk getline`:

* **When there are no redirection operators `|` or `<` on either side:** `getline` acts on the current file, reading the first line of the current file into the following variable `var` or `$0` (if no variable). Note that since awk has already read a line before processing `getline`, the result returned by `getline` is from every other line.
* **When there are redirection operators `|` or `<` on either side:** `getline` acts on the redirected input file. Since this file has just been opened and has not been read by awk yet, but only by `getline`, `getline` returns the first line of that file, not every other line.

**Examples:**

Execute the Linux `date` command and pipe the output to `getline`, then assign the output to a custom variable `out` and print it:

```shell
awk 'BEGIN{ "date" | getline out; print out }' test
```

Execute the shell `date` command, pipe the output to `getline`, then `getline` reads from the pipe and assigns the input to `out`. The `split` function converts the variable `out` into the array `mon`, and then the second element of the array `mon` is printed:

```shell
awk 'BEGIN{ "date" | getline out; split(out,mon); print mon[2] }' test
```

The output of the `ls` command is passed to `getline` as input. A loop causes `getline` to read one line from the `ls` output and print it to the screen. There is no input file here because the BEGIN block is executed before opening the input file, so the input file can be ignored.

```shell
awk 'BEGIN{ while( "ls" | getline) print }'
```

### Closing Files

awk allows closing an input or output file within the program using the `close` statement.

```shell
close("filename")
```

`filename` can be a file opened by `getline`, `stdin`, a variable containing the filename, or the exact command used by `getline`. It can also be an output file, `stdout`, a variable containing the filename, or the exact command using a pipe.

### Output to a File

awk allows outputting results to a file in the following ways:

```shell
echo | awk '{printf("hello world!\n") > "datafile"}'
# OR
echo | awk '{printf("hello world!\n") >> "datafile"}'
```

## Setting Field Delimiters

The default field delimiter is space. You can use `-F "delimiter"` to explicitly specify a delimiter:

```shell
awk -F: '{ print $NF }' /etc/passwd
# OR
awk 'BEGIN{ FS=":" } { print $NF }' /etc/passwd
```

In the **BEGIN block**, you can use `OFS="delimiter"` to set the delimiter for output fields.

## Flow Control Statements

In Linux awk's `while`, `do-while`, and `for` statements, `break` and `continue` statements are allowed to control the flow, and `exit` can be used to exit. `break` interrupts the currently executing loop and jumps to the next statement outside the loop. `if` is used for conditional selection. The syntax of flow control statements in awk is similar to C. With these statements, many shell programs can be handled by awk, and the performance is very fast. Below are the usages of each statement.

### Conditional Statements

```shell
if(expression)
  statement1
else
  statement2
```

In this format, `statement1` can be multiple statements. For convenience and readability, it's best to enclose multiple statements in `{}`. awk branch structures allow nesting, formatted as:

```shell
if(expression)
  {statement1}
else if(expression)
  {statement2}
else
  {statement3}
```

Example:

```shell
awk 'BEGIN{
test=100;
if(test>90){
  print "very good";
  }
  else if(test>60){
    print "good";
  }
  else{
    print "no pass";
  }
}'

very good
```

Each command statement can end with a `;` **semicolon**.

### Loop Statements

#### while statement

```shell
while(expression)
  {statement}
```

Example:

```shell
awk 'BEGIN{
test=100;
total=0;
while(i<=test){
  total+=i;
  i++;
}
print total;
}'
5050
```

#### for loop

There are two formats for the `for` loop:

Format 1:

```shell
for(variable in array)
  {statement}
```

Example:

```shell
awk 'BEGIN{
for(k in ENVIRON){
  print k"="ENVIRON[k];
}
}'
TERM=linux
G_BROKEN_FILENAMES=1
SHLVL=1
PWD=/root/text
...
LOGNAME=root
HOME=/root
SSH_CLIENT=192.168.1.21 53087 22
```

Note: `ENVIRON` is an awk constant and is an associative array.

Format 2:

```shell
for(variable; condition; expression)
  {statement}
```

Example:

```shell
awk 'BEGIN{
total=0;
for(i=0;i<=100;i++){
  total+=i;
}
print total;
}'
5050
```

#### do loop

```shell
do
{statement} while(condition)
```

Example:

```shell
awk 'BEGIN{ 
total=0;
i=0;
do {total+=i;i++;} while(i<=100)
  print total;
}'
5050
```

### Other Statements

* **break**: When the `break` statement is used in a `while` or `for` statement, it causes the program to exit the loop.
* **continue**: When the `continue` statement is used in a `while` or `for` statement, it causes the program to move to the next iteration of the loop.
* **next**: Can cause the reading of the next input line and return to the top of the script. This avoids executing other operations on the current input line.
* **exit**: Causes the main input loop to exit and transfers control to `END`, if `END` exists. If no `END` rule is defined, or if the `exit` statement is used within `END`, script execution terminates.

## Array Application

Arrays are the soul of awk; array processing is indispensable when dealing with text. Because array indices (subscripts) can be numbers or strings, arrays in awk are called associative arrays. Arrays in awk do not need to be declared in advance, nor do their sizes need to be declared. Array elements are initialized with 0 or an empty string, depending on the context.

### Array Definition

Using numbers as array indices (subscripts):

```shell
Array[1]="sun"
Array[2]="kai"
```

Using strings as array indices (subscripts):

```shell
Array["first"]="www"
Array["last"]="name"
Array["birth"]="1987"
```

In use, `print Array[1]` will print `sun`; `print Array[2]` will print `kai`; `print Array["birth"]` will give `1987`.

**Reading Array Values**

```shell
{ for(item in array) {print array[item]}; }       # The output order is random
{ for(i=1;i<=len;i++) {print array[i]}; }         # Len is the length of the array
```

### Array-Related Functions

**Get array length:**

```shell
awk 'BEGIN{info="it is a test";lens=split(info,tA," ");print length(tA),lens;}'
4 4
```

`length` returns the length of a string or array. `split` splits a string into an array and also returns the length of the resulting array.

```shell
awk 'BEGIN{info="it is a test";split(info,tA," ");print asort(tA);}'
4
```

`asort` sorts the array and returns the array length.

**Output array content (unordered, ordered output):**

```shell
awk 'BEGIN{info="it is a test";split(info,tA," ");for(k in tA){print k,tA[k];}}'
4 test
1 it
2 is
3 a 
```

`for…in` output is unordered by default because awk arrays are associative arrays. If you need ordered output, you must use subscripts.

```shell
awk 'BEGIN{info="it is a test";tlen=split(info,tA," ");for(k=1;k<=tlen;k++){print k,tA[k];}}'
1 it
2 is
3 a
4 test
```

Note: Array subscripts start from 1, unlike C arrays.

**Checking for key existence and deleting keys:**

```shell
# Incorrect way to check:
awk 'BEGIN{tB["a"]="a1";tB["b"]="b1";if(tB["c"]!="1"){print "not found";};for(k in tB){print k,tB[k];}}' 
not found
a a1
b b1
c
```

A strange issue occurs: `tB["c"]` was not defined, but during the loop, it's found to exist with an empty value. Note that awk arrays are associative; simply referencing a key via an array will automatically create that entry.

```shell
# Correct way to check:
awk 'BEGIN{tB["a"]="a1";tB["b"]="b1";if( "c" in tB){print "ok";};for(k in tB){print k,tB[k];}}'  
a a1
b b1
```

Use `if(key in array)` to check if an array contains the key.

```shell
# Deleting a key:
awk 'BEGIN{tB["a"]="a1";tB["b"]="b1";delete tB["a"];for(k in tB){print k,tB[k];}}'                     
b b1
```

`delete array[key]` can delete the entry corresponding to the `key` in the array.

### Using Two-Dimensional and Multi-Dimensional Arrays

Multi-dimensional arrays in awk are essentially one-dimensional arrays; more precisely, awk does not support multi-dimensional arrays for storage. awk provides a way to logically simulate multi-dimensional array access. For example, access like `array[2,4]=1` is allowed. awk uses a special string `SUBSEP (\034)` as a separator. In the example above, the key stored in the associative array `array` is actually `2\0344`.

Similar to testing members of a one-dimensional array, multi-dimensional arrays can use syntax like `if ( (i,j) in array )`, but subscripts must be placed in parentheses. Similar to looping through a one-dimensional array, multi-dimensional arrays use `for ( item in array )` syntax to traverse the array. Unlike one-dimensional arrays, multi-dimensional arrays must use the `split()` function to access individual subscript components.

```shell
awk 'BEGIN{
for(i=1;i<=9;i++){
  for(j=1;j<=9;j++){
    tarr[i,j]=i*j; print i,"*",j,"=",tarr[i,j];
  }
}
}'
1 * 1 = 1
1 * 2 = 2
1 * 3 = 3
...
9 * 9 = 81
```

Array content can be retrieved by referencing `array[k,k2]`.

Another method:

```shell
awk 'BEGIN{
for(i=1;i<=9;i++){
  for(j=1;j<=9;j++){
    tarr[i,j]=i*j;
  }
}
for(m in tarr){
  split(m,tarr2,SUBSEP); print tarr2[1],"*",tarr2[2],"=",tarr[m];
}
}'
```

## Built-in Functions

Built-in functions in awk are mainly of four types: arithmetic, string, other general functions, and time functions.

### Arithmetic Functions

| Format | Description |
| ---- | ---- |
| atan2( y, x ) | Returns the arctangent of y/x. |
| cos( x ) | Returns the cosine of x; x is in radians. |
| sin( x ) | Returns the sine of x; x is in radians. |
| exp( x ) | Returns the exponential function of x. |
| log( x ) | Returns the natural logarithm of x. |
| sqrt( x ) | Returns the square root of x. |
| int( x ) | Returns the truncated integer value of x. |
| rand( ) | Returns a random number n, where 0 <= n < 1. |
| srand( [expr] ) | Sets the seed value for the `rand` function to the value of the `expr` parameter, or uses the time of day if `expr` is omitted. Returns the previous seed value. |

Example:

```shell
awk 'BEGIN{OFMT="%.3f";fs=sin(1);fe=exp(10);fl=log(10);fi=int(3.1415);print fs,fe,fl,fi;}'
0.841 22026.466 2.303 3
```

`OFMT` sets the output data format to 3 decimal places.

Obtain random numbers:

```shell
awk 'BEGIN{srand();fr=int(100*rand());print fr;}'
78
awk 'BEGIN{srand();fr=int(100*rand());print fr;}'
31
awk 'BEGIN{srand();fr=int(100*rand());print fr;}'
41 
```

### String Functions

| Format | Description |
| ---- | ---- |
| gsub( Ere, Repl, [ In ] ) | Exactly like the `sub` function, except that all occurrences of the regular expression are replaced. |
| sub( Ere, Repl, [ In ] ) | Replaces the first occurrence of the extended regular expression specified by the `Ere` parameter in the string specified by the `In` parameter with the string specified by the `Repl` parameter. The `sub` function returns the number of replacements. `&` (ampersand) in the `Repl` string is replaced by the string matching the `Ere` regular expression. If `In` is not specified, the default is the entire record ($0). |
| index( String1, String2 ) | Returns the position (starting from 1) where `String2` first occurs in `String1`. Returns 0 if `String2` is not found. |
| length [(String)] | Returns the length (in characters) of the specified string. If `String` is not given, returns the length of the entire record ($0). |
| blength [(String)] | Returns the length (in bytes) of the specified string. If `String` is not given, returns the length of the entire record ($0). |
| substr( String, M, [ N ] ) | Returns a substring of length `N` starting at position `M` (the first character is position 1). If `N` is omitted, the substring continues to the end of `String`. |
| match( String, Ere ) | Returns the position (starting from 1) where the extended regular expression `Ere` first matches in `String`. Returns 0 if no match is found. Sets the special variable `RSTART` to the return value and `RLENGTH` to the length of the matched string (or -1 if no match). |
| split( String, A, [Ere] ) | Splits `String` into array elements `A[1], A[2], ..., A[n]` and returns the value of `n`. Splitting can be done via the regular expression `Ere` or the current field separator (`FS`). Elements in the `A` array are created as string values unless the context indicates they should also have numeric values. |
| tolower( String ) | Returns the specified string with all uppercase characters converted to lowercase. |
| toupper( String ) | Returns the specified string with all lowercase characters converted to uppercase. |
| sprintf(Format, Expression, Expression, ...) | Formats the expressions according to the `printf` subroutine format string and returns the resulting string. |

Note: `Ere` can be a regular expression.

**Using gsub and sub**

```shell
awk 'BEGIN{info="this is a test2010test!";gsub(/[0-9]+/,"!",info);print info}'
this is a test!test!
```

Finds occurrences matching `/[0-9]+/` in `info`, replaces them with `!`, and assigns the result back to `info`.

**Finding a string (using index)**

```shell
awk 'BEGIN{info="this is a test2010test!";print index(info,"test")?"ok":"not found";}'
ok
```

Returns 0 if not found.

**Regular expression matching (using match)**

```shell
awk 'BEGIN{info="this is a test2010test!";print match(info,/[0-9]+/)?"ok":"not found";}'
ok
```

**Extracting a substring (using substr)**

```shell
awk 'BEGIN{info="this is a test2010test!";print substr(info,4,10);}'
s is a tes
```

Extracts a 10-character string starting from the 4th character.

**Splitting a string (using split)**

```shell
awk 'BEGIN{info="this is a test";split(info,tA," ");print length(tA);for(k in tA){print k,tA[k];}}'
4
4 test
1 this
2 is
3 a
```

Splits `info` and dynamically creates array `tA`. Note that the `for…in` loop is unordered.

**Formatted string output (using sprintf)**

The format string includes normal characters (output as-is) and format specifications starting with `%`.

| Format | Description | Format | Description |
| ---- | ---- | ---- | ---- |
| %d | Signed decimal integer | %u | Unsigned decimal integer |
| %f | Floating-point number | %s | String |
| %c | Single character | %p | Pointer value |
| %e | Exponential floating-point | %x | %X Unsigned hexadecimal integer |
| %o | Unsigned octal integer | %g | Automatically choose best format |

```shell
awk 'BEGIN{n1=124.113;n2=-1.224;n3=1.2345; printf("%.2f,%.2u,%.2g,%X,%o\n",n1,n2,n3,n1,n1);}'
124.11,18446744073709551615,1.2,7C,174
```

### General Functions

| Format | Description |
| ---- | ---- |
| close( Expression ) | Closes a file or pipe opened by `print`, `printf`, or `getline` with the same string value `Expression`. Returns 0 if successful, non-zero otherwise. `close` is necessary if you intend to write a file and then read it later in the same program. |
| system(command) | Executes the specified command and returns the exit status. Equivalent to the `system` subroutine. |
| Expression `|` getline [ Variable ] | Reads an input record from the output of the command specified by `Expression` via a pipe, and assigns the record's value to `Variable`. If the stream is not yet open, it is created. If `Variable` is omitted, `$0` and `NF` are set. |
| getline [ Variable ] < Expression | Reads the next input record from the file specified by `Expression` and assigns it to `Variable`. If `Variable` is omitted, `$0` and `NF` are set. |
| getline [ Variable ] | Reads the next input record from the current input file and assigns it to `Variable`. If `Variable` is omitted, `$0`, `NF`, `NR`, and `FNR` are set. |

**Opening an external file (using close)**

```shell
awk 'BEGIN{while("cat /etc/passwd"|getline){print $0;};close("/etc/passwd");}'
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
```

**Reading an external file line by line (using getline)**

```shell
awk 'BEGIN{while(getline < "/etc/passwd"){print $0;};close("/etc/passwd");}'
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
```

```shell
awk 'BEGIN{print "Enter your name:";getline name;print name;}'
Enter your name:
chengmo
chengmo
```

**Calling an external application (using system)**

```shell
awk 'BEGIN{b=system("ls -al");print b;}'
total 42092
drwxr-xr-x 14 chengmo chengmo     4096 09-30 17:47 .
drwxr-xr-x 95 root   root       4096 10-08 14:01 ..
```

The value of `b` is the exit status of the execution.

### Time Functions

| Format | Description |
| ---- | ---- |
| mktime( YYYY MM dd HH MM ss[ DST]) | Generates a time format. |
| strftime([format [, timestamp]]) | Formats time output, converting a timestamp to a formatted time string. |
| systime() | Returns the current timestamp (seconds since January 1, 1970). |

**Creating a specific time (using mktime)**

```shell
awk 'BEGIN{tstamp=mktime("2001 01 01 12 12 12");print strftime("%c",tstamp);}'
Mon Jan  1 12:12:12 2001
```

```shell
awk 'BEGIN{tstamp1=mktime("2001 01 01 12 12 12");tstamp2=mktime("2001 02 01 0 0 0");print tstamp2-tstamp1;}'
2634468
```

Calculates the time difference between two time points.

```shell
awk 'BEGIN{tstamp1=mktime("2001 01 01 12 12 12");tstamp2=systime();print tstamp2-tstamp1;}' 
308201392
```

**strftime Date and Time Format Specifiers**

| Format | Description |
| ---- | ---- |
| %a | Abbreviated weekday name (Sun) |
| %A | Full weekday name (Sunday) |
| %b | Abbreviated month name (Oct) |
| %B | Full month name (October) |
| %c | Local date and time |
| %d | Decimal date (01-31) |
| %D | Date (08/20/99) |
| %e | Date, padded with a space if single digit |
| %H | Hour in 24-hour format |
| %I | Hour in 12-hour format |
| %j | Day of the year (001-366) |
| %m | Month (01-12) |
| %M | Minute (00-59) |
| %p | 12-hour notation (AM/PM) |
| %S | Second (00-59) |
| %U | Week number of the year (Sunday as first day of week) |
| %w | Weekday (Sunday is 0) |
| %W | Week number of the year (Monday as first day of week) |
| %x | Local date (08/20/99) |
| %X | Local time (12:00:00) |
| %y | Two-digit year (99) |
| %Y | Full year |
| %% | Percent sign (%) |
