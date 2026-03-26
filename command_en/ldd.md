ldd
===

Print shared library dependencies of a program or library

## Description

The **ldd** command is used to print the list of shared libraries that a program or library file depends on.

### Syntax

```shell
ldd (options) (parameters)
```

### Options

```shell
--version: Print the version number;
-v: Verbose mode, print all related information;
-u: Print unused direct dependencies;
-d: Perform relocations and report any missing objects;
-r: Perform relocations for both data objects and functions, and report any missing objects or functions;
--help: Display help information.
```

### Parameters

File: Specify the executable program or library file.

### Further Information

First, `ldd` is not an executable binary, but a shell script.

`ldd` displays the dependencies of an executable module by setting a series of environment variables, such as: `LD_TRACE_LOADED_OBJECTS`, `LD_WARN`, `LD_BIND_NOW`, `LD_LIBRARY_VERSION`, `LD_VERBOSE`, etc. When the `LD_TRACE_LOADED_OBJECTS` environment variable is not empty, any executable program will only display its module dependencies upon execution, without actually running the program. You can test this in a shell terminal:

```shell
export LD_TRACE_LOADED_OBJECTS=1
```

Then try running any program, like `ls`, and observe the result.

The principle behind `ldd`'s dependency display is actually implemented by `ld-linux.so` (the ELF dynamic library loader). We know that the `ld-linux.so` module runs before the executable program and gains control; therefore, when the aforementioned environment variables are set, `ld-linux.so` chooses to display the executable's dependencies.

In fact, you can execute the `ld-linux.so` module directly, for example: `/lib/ld-linux.so.2 --list program` (which is equivalent to `ldd program`).
