figlet
===

Convert strings into "ASCII art" characters.

## Description

Converts ordinary strings into "ASCII art" characters composed of simple characters.

## Installation

For Ubuntu and similar systems:

```shell
apt-get update
apt-get install -y figlet
```

For CentOS and similar systems:

```shell
yum install epel-release
yum install -y figlet
```

## Syntax

```shell
figlet [ message ] [ -option ]
```

## Parameters

`message` is the string that needs to be converted.
If no `message` is provided, it reads from standard input, making it compatible with pipes and other redirections.

## Options

```shell
-w      Limit output width, defaults to '80'.
-c      Center the output.
-f      Specify the font, defaults to 'standard'.
-k      Keep whitespace between characters.
-t      Align width to the current terminal width; this parameter takes precedence over -w.
-v      Display version information.
```

## Return Value

A string representing the "ASCII art" composed of simple characters.

## Examples

### Input from Parameters

```shell
figlet 'Hello, World!'
```

```bash
 _   _      _ _         __        __         _     _ _
| | | | ___| | | ___    \ \      / /__  _ __| | __| | |
| |_| |/ _ \ | |/ _ \    \ \ /\ / / _ \| '__| |/ _` | |
|  _  |  __/ | | (_) |    \ V  V / (_) | |  | | (_| |_|
|_| |_|\___|_|_|\___( )    \_/\_/ \___/|_|  |_|\__,_(_)
```

### Input via Pipe

```shell
echo 'Hello, World!' | figlet
```

```bash
 _   _      _ _         __        __         _     _ _
| | | | ___| | | ___    \ \      / /__  _ __| | __| | |
| |_| |/ _ \ | |/ _ \    \ \ /\ / / _ \| '__| |/ _` | |
|  _  |  __/ | | (_) |    \ V  V / (_) | |  | | (_| |_|
|_| |_|\___|_|_|\___( )    \_/\_/ \___/|_|  |_|\__,_(_)
```

### Limit Width

```shell
figlet 'Hello, World!' -w 40
```

```bash
 _   _      _ _
| | | | ___| | | ___
| |_| |/ _ \ | |/ _ \
|  _  |  __/ | | (_) |
|_| |_|\___|_|_|\___( )
                    |/
__        __         _     _ _
\ \      / /__  _ __| | __| | |
 \ \ /\ / / _ \| '__| |/ _` | |
  \ V  V / (_) | |  | | (_| |_|
   \_/\_/ \___/|_|  |_|\__,_(_)
```

### Center Output

```shell
figlet 'Hello, World!' -w 40 -c
```

```bash
         _   _      _ _
        | | | | ___| | | ___
        | |_| |/ _ \ | |/ _ \
        |  _  |  __/ | | (_) |
        |_| |_|\___|_|_|\___( )
                            |/
    __        __         _     _ _
    \ \      / /__  _ __| | __| | |
     \ \ /\ / / _ \| '__| |/ _` | |
      \ V  V / (_) | |  | | (_| |_|
       \_/\_/ \___/|_|  |_|\__,_(_)
```

### Specify Font

```shell
figlet 'Hello, World!' -w 40 -c -f slant
```

```bash
            __  __     ____
           / / / /__  / / /___
          / /_/ / _ \/ / / __ \
         / __  /  __/ / / /_/ /
        /_/ /_/\___/_/_/\____( )
                             |/
     _       __           __    ____
    | |     / /___  _____/ /___/ / /
    | | /| / / __ \/ ___/ / __  / /
    | |/ |/ / /_/ / /  / / /_/ /_/
    |__/|__/\____/_/  /_/\__,_(_)
```

### Keep Whitespace Between Characters

```shell
figlet 'Hello, World!' -w 40 -c -k
```

```bash
       _   _        _  _
      | | | |  ___ | || |  ___
      | |_| | / _ \| || | / _ \
      |  _  ||  __/| || || (_) |_
      |_| |_| \___||_||_| \___/( )
                               |/
  __        __            _      _  _
  \ \      / /___   _ __ | |  __| || |
   \ \ /\ / // _ \ | '__|| | / _` || |
    \ V  V /| (_) || |   | || (_| ||_|
     \_/\_/  \___/ |_|   |_| \__,_|(_)
```
