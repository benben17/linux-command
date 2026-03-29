# Contributor Guidelines

Thank you for your contributions to this project. To help maintainers manage effectively, please follow these conventions:

## If You Want to Submit a Command

Commands are stored in the `./command/` directory:

1. Create a `[CommandName].md` file, e.g., `pacman.md`
2. Open the file and type the command as it would be executed in the terminal
3. Enter three equals signs on the second line
4. Create a second-level heading "Additional Notes," and under this heading create at least the following third-level headings:
- Syntax
- Options
- Parameters

Expected document structure:

```markdown
CommandName
===

This is the command description. It can be searched. If you have a popular application with multiple commands, you can include them here to enable searching for the corresponding commands.

## Additional Notes

**CommandName command** is used for demonstration purposes.

### Syntax

(When writing the actual documentation, please wrap the following in a shell code block)

CommandName <-abcdABCD> <required parameter> [optional parameter]

### Options

(When writing the actual documentation, please wrap the following in a shell code block)

-a xxxxx
-b xxxxx
...
-C xxxxx
-D xxxxx

### Parameters

(When writing the actual documentation, please wrap the following in a shell code block)

Optional parameter: Generally can be omitted

```

## If You Want to Maintain the Frontend Pages

- Ensure your code runs completely in the latest Chromium and Safari browsers (#489)

## Other Commit Message Conventions

- Conventional Commits <https://www.conventionalcommits.org/en/v1.0.0/>
- Chinese Copywriting Guidelines <https://github.com/sparanoid/chinese-copywriting-guidelines/blob/master/README.zh-Hans.md>
- Preface — Google Open Source Project Style Guide <https://zh-google-styleguide.readthedocs.io/en/latest/google-shell-styleguide/>
