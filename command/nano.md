nano
===

Character-based terminal text editor

## Description

**nano** is a text editor for terminal environments, similar to the `editor` program in DOS. It is much simpler than `vi`/`vim`, making it very suitable for Linux beginners. Some Linux distributions use `nano` as their default editor.

The `nano` command opens a specified file for editing. By default, it automatically wraps lines (breaks long lines into multiple lines). However, this can cause issues with certain files, such as Linux system configurations, where a single logical line might be broken into multiple lines, potentially causing system errors. To avoid this, use the `-w` option.

### Syntax

```shell
nano [options] [[+line,column] filename]...
```

### Options

```shell
 -h, -?         --help                  Display this help message.
 +line,column                           Start at the specified line and column.
 -A             --smarthome             Enable smart HOME key.
 -B             --backup                Save a backup of the existing file.
 -C <dir>       --backupdir=<dir>       Directory to store backup files.
 -D             --boldtext              Use bold text instead of reverse video.
 -E             --tabstospaces          Convert typed tabs to spaces.
 -F             --multibuffer           Enable multiple file buffers.
 -H             --historylog            Log and read search/replace history strings.
 -I             --ignorercfiles         Don't look at nanorc files.
 -K             --rebindkeypad          Fix numeric keypad confusion.
 -L             --nonewlines            Don't add newlines to the end of files.
 -N             --noconvert             Don't convert from DOS/Mac format.
 -O             --morespace             Use one extra line for editing.
 -Q <str>       --quotestr=<str>        Quotation string.
 -R             --restricted            Restricted mode.
 -S             --smooth                Smooth scrolling (by lines).
 -T <#cols>     --tabsize=<#cols>       Set width of a tab to #cols.
 -U             --quickblank            Do quick statusbar blanking.
 -V             --version               Display version information and exit.
 -W             --wordbounds            Detect word boundaries more accurately.
 -Y <str>       --syntax=<str>          Syntax definition to use for highlighting.
 -c             --const                 Constantly show cursor position.
 -d             --rebinddelete          Fix Backspace/Delete confusion.
 -i             --autoindent            Automatically indent new lines.
 -k             --cut                   Cut from cursor to end of line.
 -l             --nofollow              Don't follow symbolic links, overwrite them.
 -m             --mouse                 Enable mouse support.
 -o <dir>       --operatingdir=<dir>    Set operating directory.
 -p             --preserve              Preserve XON (^Q) and XOFF (^S) keys.
 -q             --quiet                 Silently ignore startup problems (e.g., rc file errors).
 -r <#cols>     --fill=<#cols>          Set hard-wrap width to #cols.
 -s <prog>      --speller=<prog>        Enable alternative spell checker.
 -t             --tempfile              Auto-save on exit, don't prompt.
 -u             --undo                  Allow generic undo [experimental].
 -v             --view                  View mode (read-only).
 -w             --nowrap                Don't hard-wrap long lines.
 -x             --nohelp                Don't show help window.
 -z             --suspend               Enable suspension.
 -$             --softwrap              Enable soft line wrapping.
 -a, -b, -e,
 -f, -g, -j                             (Ignored for compatibility with pico)
```

### Usage

**Cursor Control**

* Move cursor: Use arrow keys.
* Select text: Click and drag with the left mouse button.

**Copy, Cut, and Paste**

* Copy an entire line: `Alt+6`
* Cut an entire line: `Ctrl+K`
* Paste: `Ctrl+U`

To copy/cut multiple lines or a part of a line, move the cursor to the beginning of the text, press `Ctrl+6` (or `Alt+A`) to mark it, then move the cursor to the end. The selected text will be highlighted. Use `Alt+6` to copy or `Ctrl+K` to cut. To cancel the selection, press `Ctrl+6` again.

**Search**

Press `Ctrl+W`, enter your search term, and press `Enter`. This will jump to the first match. Use `Alt+W` to jump to the next match.

**Paging**

* `Ctrl+Y`: Previous page.
* `Ctrl+V`: Next page.

**Save**

Press `Ctrl+O` to save changes.

**Exit**

Press `Ctrl+X`.

If you have modified the file, you will be asked whether to save changes. Press `Y` for yes, `N` for no, or `Ctrl+C` to cancel and return to editing. If you press `Y`, you will be prompted for a filename. Press `Enter` to keep the current name or enter a new name to "Save As". You can also use `Ctrl+C` to cancel here.
