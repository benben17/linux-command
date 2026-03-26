xlsfonts
===

List fonts used by the X Server.

## Supplemental Information

The **xlsfonts command** lists the fonts used by the X Server. You can also use pattern matching to list only those fonts that meet specific criteria.

### Syntax

```shell
xlsfonts(options)
```

### Options

```shell
-l: List font properties in addition to font names.
-ll: Similar to "-l", but provides more detailed information.
-lll: Similar to "-ll", but provides even more detailed information.
-m: When used with "-l", lists the upper and lower bounds of font size as well.
-n <columns>: Set the number of columns to display per line.
-o: List the font inventory in OpenFont format.
-u: Do not sort the font list by name.
-w <characters_per_line>: Set the maximum number of characters per line.
```
