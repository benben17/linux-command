unexpand
===

Convert spaces in files to tabs.

## Description

The **unexpand command** is used to convert whitespace (spaces) in a given file into tabs (TAB) and display the conversion result on the standard output device (terminal).

### Syntax

```shell
unexpand (option) (parameter)
```

### Options

```shell
-a or --all: Convert all whitespace characters in the file;
--first-only: Only convert leading whitespace characters;
-t<N>: Specify that a TAB represents N characters (N is an integer), the default value of N is 8.
```

### Parameters

File: Specifies the list of files where spaces should be converted to tabs.
