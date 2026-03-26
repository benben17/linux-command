tload
===

Display system load average

## Description

The **tload command** graphically outputs the current system load average to a specified terminal. If no terminal number is given, the load situation is displayed on the terminal where the tload instruction is executed.

### Syntax

```shell
tload [options] [parameters]
```

### Options

```shell
-s: Specify the scale for idle time;
-d: Specify the interval time (seconds).
```

### Parameters

Terminal: Specifies the terminal device file to display the information.

### Examples

Use the tload command to view system load:

```shell
tload -d 1
0.08, 0.02, 0.01
0.04, 0.01, 0.00
0.04, 0.01, 0.00
0.04, 0.01, 0.00
0.06, 0.02, 0.00
```
