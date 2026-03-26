xlsatoms
===

List all defined atom names on the X server.

## Supplemental Information

The **xlsatoms command** is used to list all defined atom names on the X server, each with its own ID. You can use options to set the list range or directly specify the name of the atom to query.

### Syntax

```shell
xlsatoms(options)
```

### Options

* -display <display_id>: Specify the display number for connecting to the X Server, starting from "0" and incrementing sequentially.
* -format <output_format>: Set the format for the atom list; you can use control characters to change the display style.
* -name <atom_name>: List a specific atom.
* -range <list_range>: Set the list range for the atom list.
