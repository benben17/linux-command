php
===

Command-line interface for the PHP language.

## Description

The **php command** is the command-line interface for PHP, a popular web development language. It allows developers to create and execute PHP scripts for system administration, batch processing, or other non-web tasks.

### Syntax

```shell
php [options] [file] [--] [arguments...]
```

### Options

```shell
-a: Enter interactive mode (REPL).
-c <path>: Specify the directory where "php.ini" is located.
-d foo[=bar]: Define INI entry 'foo' with value 'bar'.
-f <file>: Parse and execute <file>.
-h: Display help.
-i: Display PHP information (like phpinfo()).
-l: Syntax check only (lint).
-m: Show compiled-in modules.
-r <code>: Run PHP <code> without using script tags <?php ... ?>.
-v: Display version information.
```

### Parameters

File: The PHP script to execute.
