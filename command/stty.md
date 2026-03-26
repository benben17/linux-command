stty
===

Modify terminal command line settings

## Description

The **stty command** is used to change and print terminal line settings.

### Syntax

```shell
stty (options) (parameters)
```

### Options

```shell
-a: Print all current settings in a human-readable format.
-g: Print all current settings in a format readable by stty.
```

### Parameters

Terminal settings: Specify terminal command line setting options.

### Examples

**Disable uppercase output on the command line:**

```shell
stty iuclc     # Enable
stty -iuclc    # Restore
```

**Disable lowercase output on the command line:**

```shell
stty olcuc    # Enable
stty -olcuc   # Restore
```

**Print terminal rows and columns:**

```shell
stty size
```

**Change the Ctrl+D (EOF) key:**

```shell
stty eof "string"
```

The system defaults to Ctrl+D to indicate EOF; this method allows you to change it.

**Toggle echoing:**

```shell
stty -echo   # Disable echo
stty echo    # Enable echo
```

Test method:

```shell
stty -echo; read; stty echo; read
```

**Ignore carriage returns:**

```shell
stty igncr     # Enable
stty -igncr    # Restore
```

**Timed input:**

```shell
timeout_read()
{
    timeout=$1
    old_stty_settings=`stty -g`    # Save current settings
    stty -icanon min 0 time 100    # Set to 10 seconds (time is in deciseconds)
    eval read varname              # Read into varname
    stty "$old_stty_settings"      # Recover settings
}
```

A simpler method is using the `-t` option of the `read` command:

```shell
read -t 10 varname
```
