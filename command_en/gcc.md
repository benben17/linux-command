gcc
===

GNU Project C and C++ compiler.

## Description

The **gcc command** invokes the GNU C/C++ compiler, which is the most widely used compiler in the open-source community. It is powerful and supports various performance optimizations. `GCC` can be used to compile programs in languages such as C, C++, Fortran, Java, Objective-C, and Ada, depending on the installed language support.

### Syntax

```shell
gcc (options) (parameters)
```

### Options

```shell
-o: Specify the name of the output file.
-E: Stop after the preprocessing stage; do not run the compiler proper.
-S: Stop after the stage of compilation proper; do not assemble.
-Wall: Enable all compiler warning messages.
-c: Compile or assemble the source files, but do not link.
-l: Link with a specified library (the library name follows -l).
-I: Add a directory to the list of directories to be searched for header files.
```

### Parameters

C Source File: Specifies the C language source code file(s).

### Examples

**Common Compilation Options**

Assuming the source file is `test.c`.

**Compile and link without options:**

```shell
gcc test.c
```

This preprocesses, assembles, compiles, and links `test.c` into an executable. Since no output file is specified, the default is `a.out`.

**Option -o:**

```shell
gcc test.c -o test
```

Preprocesses, assembles, compiles, and links `test.c` into an executable named `test`.

**Option -E:**

```shell
gcc -E test.c -o test.i
```

Preprocesses `test.c` and outputs the result to `test.i`.

**Option -S:**

```shell
gcc -S test.i
```

Compiles the preprocessed file `test.i` into assembly code in `test.s`.

**Option -c:**

```shell
gcc -c test.s
```

Assembles the file `test.s` into an object file `test.o`.

**Linking without further options:**

```shell
gcc test.o -o test
```

Links the object file `test.o` into the final executable `test`.

**Option -O:**

```shell
gcc -O1 test.c -o test
```

Compiles the program with optimization level 1. Levels range from 1 to 3; higher levels provide better optimization but increase compilation time.

**Compiling Multiple Source Files**

There are two main ways to compile multiple source files (e.g., `test.c` and `testfun.c`).

**Compile all files together:**

```shell
gcc testfun.c test.c -o test
```

Compiles and links both files into a single executable `test`.

**Compile separately and then link:**

```shell
gcc -c testfun.c    # Compiles testfun.c into testfun.o
gcc -c test.c       # Compiles test.c into test.o
gcc testfun.o test.o -o test   # Links both object files into test
```

Comparison: The first method requires all files to be recompiled every time. The second method allows you to recompile only the modified files, saving time on large projects.

**Link with a dynamic library:**

```shell
gcc hello.c -lpthread -o hello
```

**Add a custom include path:**

```shell
gcc hello.c -lpthread -I /lib64/ -o hello
```
