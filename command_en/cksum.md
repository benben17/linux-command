cksum
===

Check the CRC checksum of files

## Description

The **cksum command** checks the Cyclic Redundancy Check (CRC) of a file to ensure it has not been corrupted during transfer from one system to another. This method requires the checksum to be calculated on the source system and again on the destination system. If the two numbers match, the file is considered correctly transferred.

Note: CRC is an error-checking method known as Cyclic Redundancy Check.

When a specified file is checked by the `cksum` command, it returns the check results for the user to verify the file's integrity. If no file name is specified or if the file name is "-", the `cksum` command reads data from standard input.

### Syntax

```shell
cksum [options] [arguments]
```

### Options

```shell
--help: Online help;
--version: Display version information.
```

### Arguments

File: Specify the file(s) to calculate the checksum for.

### Examples

Use the `cksum` command to calculate the integrity of the file "testfile1":

```shell
cksum testfile1            # Perform CRC check on the specified file
```

After executing the above command, the checksum and related information will be output as follows:

```shell
1263453430 78 testfile1     # Output information
```

In the output, "1263453430" represents the checksum, and "78" represents the number of bytes.

Note: If any character in the file is modified, the calculated CRC checksum value will change.
