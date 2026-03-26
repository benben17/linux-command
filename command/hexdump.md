hexdump
===

Display file contents in hexadecimal format.

## Supplemental Information

The **hexdump command** is typically used to view the hexadecimal encoding of binary files, but it can actually be used to view any file.

### Syntax

```shell
hexdump [options] [file]...
```

### Options

```shell
-n length    # Interpret only length bytes of input.
-C           # Canonical hex+ASCII display.
-b           # One-byte octal display.
-c           # One-byte character display.
-d           # Two-byte decimal display.
-o           # Two-byte octal display.
-x           # Two-byte hexadecimal display.
-s offset    # Skip offset bytes from the beginning of the input.
-e format    # Specify a format string for displaying data. The format string is enclosed in single quotes and follows the pattern: 'a/b "format1" "format2"'.
```

Each format string consists of three parts separated by spaces:
1. `a/b`: `b` specifies the number of bytes to apply `format1` to, and `a` specifies the number of bytes to apply `format2` to. Typically `a > b`, and `b` can only be 1, 2, or 4. `a` is optional; if omitted, it defaults to 1.
2. `format1` and `format2` can use `printf`-style format strings:
   - `%02d`: Two-digit decimal
   - `%03x`: Three-digit hexadecimal
   - `%02o`: Two-digit octal
   - `%c`: Single character

Special sequences:
- `%_ad`: Display the address (byte offset) in decimal.
- `%_ax`: Display the address in hexadecimal.
- `%_ao`: Display the address in octal.
- `%_p`: For non-printing characters, display a dot (.).

Multiple `-e` options can be used to display multiple format strings per line.

### Examples

```shell
hexdump -e '16/1 "%02X " "  |  "' -e '16/1 "%_p" "\n"' test
00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F  |  ................  
10 11 12 13 14 15 16 17 18 19 1A 1B 1C 1D 1E 1F  |  ................  
20 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F  |   !"#$%&'()*+,-./ 
```
