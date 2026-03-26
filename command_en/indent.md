indent
===

Format C language source files.

## Description

The `indent` command recognizes C source code files and formats them to make them easier for programmers to read and modify.

### Syntax

```shell
indent [options] [source_file]
# or
indent [options] [source_file] [-o output_file]
```

### Options

```shell
-bad : Add blank lines after declarations.
-bap : Add blank lines after procedure bodies.
-bbb : Add blank lines after comments.
-bc : Force newlines after commas in declarations.
-bl : Put braces on lines after if (or else, for, etc.) and indent them.
-bli<n> : Set the indentation for braces by n spaces.
-br : Put braces on the same line as if (or else, for, etc.).
-bs : Put a space after sizeof.
-c<n> : Put comments to the right of code in column n.
-cd<n> : Put comments to the right of declarations in column n.
-cdb : Put comment delimiters on blank lines.
-ce : Cuddle else and the preceding '}'.
-ci<n> : Set continuation indentation to n spaces.
-cli<n> : Set case label indentation to n spaces.
-cp<n> : Put comments to the right of #else and #endif in column n.
-cs : Put a space after a cast operator.
-d<n> : Set indentation of comments not to the right of code to n spaces.
-di<n> : Set indentation of variables in declarations to column n.
-fc1 : Format comments that start in column 1.
-fca : Format all comments.
-gnu : Use GNU formatting style (default).
-i<n> : Set indentation level to n spaces.
-ip<n> : Set parameter indentation to n spaces.
-kr : Use Kernighan & Ritchie formatting style.
-lp : Line up continued lines at parentheses.
-nbad : Do not add blank lines after declarations.
-nbap : Do not add blank lines after procedure bodies.
-nbbb : Do not add blank lines after comments.
-nbc : Do not force newlines after commas in declarations.
-ncdb : Do not put comment delimiters on blank lines.
-nce : Do not cuddle else.
-ncs : Do not put a space after a cast operator.
-nfc1 : Do not format comments that start in column 1.
-nfca : Do not format any comments.
-nip : Do not indent parameters.
-nlp : Do not line up continued lines at parentheses.
-npcs : Do not put a space after the function name in a call.
-npro : Do not read the `.indent.pro` profile.
-npsl : Put the return type on the same line as the function name.
-nsc : Do not put stars on the left side of comments.
-nsob : Do not swallow optional blank lines.
-nss : Do not put a space before the semicolon in certain statements.
-nv : Disable verbose mode.
-orig : Use Berkeley formatting style.
-pcs : Put a space between the function name and '(' in a call.
-psl : Put the return type on the line before the function name.
-sc : Put stars on the left side of comments.
-sob : Swallow optional blank lines.
-ss : Put a space before the semicolon in for and while statements.
-st : Write output to standard output.
-T : Specify a type name for indentation.
-ts<n> : Set tab size to n spaces.
-v : Enable verbose mode.
--version : Display version information.
```

### Examples

To add a space after all occurrences of `sizeof` in a C source file `test.c`:

```shell
indent -bs /home/user/desktop/test.c
```

After running this, the specified source file will be modified. Since there are many parameters, choose the ones that best fit your needs.
