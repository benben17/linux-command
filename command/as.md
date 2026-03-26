as
===

Assembler for assembly language

## Additional Information

The **as command** is an assembly language compiler released by the GNU organization, supporting many different types of processors.

### Syntax

```shell
as [options] [parameters]
```

### Options

```shell
-ac: Ignore failure conditions.
-ad: Ignore debug directives.
-ah: Include high-level source.
-al: Include assembly.
-am: Include macro expansions.
-an: Ignore formal processing.
-as: Include symbols.
=file: Set the name of the listing file.
--alternate: Start in alternate macro mode.
-f: Skip whitespace and comment preprocessing.
-g: Generate debug information.
-J: Do not display warnings for signed overflow.
-L: Retain local symbols in the symbol table.
-o: Specify the object file to generate.
--statistics: Print the maximum space and total time used for assembly.
```

### Parameters

Assembly file: Specifies the source file to be assembled.

### Examples

Assemble an assembly file and generate an object file:

```shell
as -o output.o source.s
```

Ignore debug directives and generate an object file:

```shell
as -ad -o output.o source.s
```

Generate an object file with debug information:

```shell
as -g -o output.o source.s
```

Include macro expansions and generate an object file:

```shell
as -am -o output.o source.s
```

Print the maximum space and total time used for assembly:

```shell
as --statistics -o output.o source.s
```

Skip whitespace and comment preprocessing and generate an object file:

```shell
as -f -o output.o source.s
```
