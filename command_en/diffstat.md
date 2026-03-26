diffstat
===

Make a histogram from diff output.

## Description

The **diffstat** command reads the output of the `diff` command and displays a histogram of the insertions, deletions, and modifications per file. It provides a summary of the differences between files. Users can also pipe the output of `diff` directly to `diffstat`. If the files or directories being compared are not in the current directory, absolute paths should be used.

### Syntax

```shell
diffstat (options) (parameters)
```

### Options

```shell
-n <length>   Specify the maximum filename length. It must be greater than or equal to the longest filename.
-p <length>   Same as -n, but <length> includes the file path.
-w            Specify the width of the output field.
-v            Display version information.
```

### Parameters

File: Specifies the file containing the output from the `diff` command.

### Examples

Compare files with the same name "testf.txt" in directories "test1" and "test2" using `diff`, and then use `diffstat` to display the statistics:

```shell
diff test1 test2 | diffstat    # Display statistical results
```

Note: This command is very convenient for viewing a summary of changes.

You can view the content of the files using the `cat` command:

```shell
cat test1/testf.txt           # View content of test1/testf
abc
def
ghi
jkl
mno
pqr
stu
vws

cat test2/testf.txt          # View content of test2/testf
abc
def
ghi
jkl
mno
```

From the content above, we can see the differences. Now run the previous command to see the statistics:

```shell
testfile | 2 +-             # Statistical information output
1 file changed, 1 insertion(+), 1 deletion(-)
```
