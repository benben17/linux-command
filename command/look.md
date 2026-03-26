look
===

Display lines in a file that begin with a specified string

## Description

The **look** command is used to display any lines in a file that start with the specified string.

### Syntax

```shell
look (options) (parameters)
```

### Options

```shell
-a: Use the alternative dictionary file `web2` located in `/usr/dict`;
-d: Use dictionary order (compare only alphanumeric characters);
-f: Ignore case distinctions;
-t <string>: Specify a termination character (ignore characters after the first occurrence of the string).
```

### Parameters

*   String: The string to search for at the beginning of lines;
*   File: The file to search in.
