ag
===

An upgraded version of ack, written in C. Faster and more user-friendly.


## Description

> Excerpted from the Readme.md of the <https://github.com/ggreer/the_silver_searcher> project.

- It is an order of magnitude faster than ack.
- It ignores file patterns in your `.gitignore` and `.hgignore`.
- If there are files in your source repository you don't want to search, just add their patterns to a `.ignore` file. (*cough* *.min.js* *cough*)
- The command name is 33% shorter than ack, and all the keys are on the home row!

### Syntax

```shell
ag [options] pattern [path ...]
```

### Options

```shell
Output Options:
     --ackmate            Display results in AckMate-parseable format.
  -A --after [LINES]      Print LINES of context after matches. (Default: 2)
  -B --before [LINES]     Print LINES of context before matches. (Default: 2)
     --[no]break          Print a newline between matches in different files. (Enabled by default)
  -c --count              Only print the number of matches in each file. (This often differs from the number of matching lines)
     --[no]color          Print color codes in results. (Enabled by default)
     --color-line-number  Color code for line numbers. (Default: 1;33)
     --color-match        Color code for result matches. (Default: 30;43)
     --color-path         Color code for path names. (Default: 1;32)
     --column             Print column numbers in results.
     --[no]filename       Print file names (enabled unless searching a single file).
  -H --[no]heading        Print file names above each file's results. (Enabled by default)
  -C --context [LINES]    Print LINES of context above and below matches. (Default: 2)
     --[no]group          Same as: --[no]break --[no]heading.
  -g --filename-pattern PATTERN Print filenames matching PATTERN.
  -l --files-with-matches Only print filenames that contain matches.
  -L --files-without-matches Only print filenames that do not contain matches.
     --print-all-files    Print headings for all files searched, even those without matches.
     --[no]numbers        Print line numbers. Default is to omit line numbers when searching a stream.
  -o --only-matching      Only print the matching part of each line.
     --print-long-lines   Print matches on very long lines (Default: >2k characters).
     --passthrough        When searching a stream, print all lines even if they don't match.
     --silent             Suppress all log messages, including errors.
     --stats              Print statistics (files scanned, time taken, etc.).
     --stats-only         Print statistics and nothing else (same as --count when searching a single file).
     --vimgrep            Print results like vim's :vimgrep /pattern/g (reports every match on every line).
  -0 --null --print0      Separate filenames with a null character (useful for 'xargs -0').

Search Options:
  -a --all-types          Search all files (including hidden files).
  -D --debug              Ridiculous debugging (likely not useful).
     --depth NUM          Maximum directory search depth. (Default: 25)
  -f --follow             Follow symlinks.
  -F --fixed-strings      Alias for --literal for compatibility with grep.
  -G --file-search-regex  Search files whose names match a regex.
     --hidden             Search hidden files (but respect .*ignore files).
  -i --ignore-case        Match case-insensitively.
     --ignore PATTERN     Ignore files/directories matching PATTERN (literal names also allowed).
     --ignore-dir NAME    Alias for --ignore for compatibility with ack.
  -m --max-count NUM      Maximum number of matches in a single file. (Default: 10,000)
     --one-device         Do not follow links to other devices.
  -p --path-to-ignore STRING Use .ignore file at STRING.
  -Q --literal            Do not parse PATTERN as a regular expression.
  -s --case-sensitive     Match case-sensitively.
  -S --smart-case         Match case-insensitively unless PATTERN contains uppercase characters.
     --search-binary      Search binary files.
  -t --all-text           Search all text files (excludes hidden files).
  -u --unrestricted       Search all files (ignores .ignore, .gitignore, etc.; searches binary and hidden files).
  -U --skip-vcs-ignores   Ignore VCS ignore files (.gitignore, .hgignore, etc.; still respects .ignore).
  -v --invert-match       Invert match (select non-matching lines).
  -w --word-regexp        Only match whole words.
  -W --width NUM          Truncate matching lines after NUM characters.
  -z --search-zip         Search contents of compressed files.

File Types:
Search can be limited to certain types of files, for example:
   ag --html needle   # Search for "needle" in files ending in .htm, .html, .shtml, or .xhtml

For a list of supported file types, run:
  ag --list-file-types
```

### Examples

List files in the current directory containing `npm`:

```shell
➜  vue-project ag npm ./
README.md
16:npm install
22:npm run dev
28:npm run build
```
