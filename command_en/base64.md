base64
===

Base64 encode/decode files or standard input/output.

### Description

`base64` encodes or decodes `FILE`, or standard input, to standard output.

### Syntax

```shell
base64 [OPTION]... [FILE]
```

### Options

```shell
-d, --decode         # Decode data
-i, --ignore-garbage # When decoding, ignore non-alphabetic characters
-w, --wrap=COLS      # Wrap encoded lines after COLS character (default 76). Use 0 to disable line wrapping

--help               # Display this help and exit
--version            # Output version information and exit
```

### Examples

Encode a string:

```bash
printf foo | base64
```

Encode a file:

```bash
base64 file
```

Decode a string:

```bash
printf Zm9v | base64 -d
```

Decode a file:

```bash
base64 -d file
```
