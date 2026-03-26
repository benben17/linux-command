fmt
===

Format text files for optimal output.

## Description

The **fmt command** reads the content of a file, performs simple formatting optimizations based on specified options, and sends the result to standard output.

### Syntax

```shell
fmt (options) (parameters)
```

### Options

```shell
-c, --crown-margin: Preserve the indentation of the first two lines of each paragraph.
-p <string>, --prefix=<string>: Only reformat lines beginning with the specified string. This is often used for formatting comments in source code.
-s, --split-only: Split long lines but do not join short lines.
-t, --tagged-paragraph: Indentation of the first line of a paragraph is different from the rest.
-u, --uniform-spacing: Use one space between words and two spaces between sentences.
-w <width>, --width=<width>: Set the maximum line width (default is 75).
```

### Parameters

Specifies the file to be reformatted.
