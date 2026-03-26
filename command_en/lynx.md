lynx
===

A text-mode web browser

## Description

The **lynx command** is a text-mode web browser for the World Wide Web. It does not support graphics, audio, video, or other multimedia content.

### Syntax

```shell
lynx [OPTION]... [URL]
```

### Options

```shell
-case：Enable case-sensitive string searching.
-ftp：Disable FTP support.
-nobrowse：Disable directory browsing.
-nocolor：Disable color mode.
-reload：Flush the proxy cache (only affects the first page).
--color：Enable color mode if supported by the system.
--help：Display help information.
--version：Display version information.
```

### Parameters

URL: The URL of the website or file to access.

## Internal Commands

**Navigation Commands**

```shell
Down Arrow: Next link on the page (highlighted).
Up Arrow: Previous link on the page (highlighted).
Enter or Right Arrow: Follow the highlighted link.
Left Arrow: Go back to the previous page.
```

**Scrolling Commands**

```shell
+, Page-Down, Space, Ctrl+f: Scroll down one page.
-, Page-Up, b, Ctrl+b: Scroll up one page.
Ctrl+a: Go to the beginning of the current page.
Ctrl+e: Go to the end of the current page.
Ctrl+n: Scroll down two lines.
Ctrl+p: Scroll up two lines.
): Scroll down half a page.
(: Scroll up half a page.
#: Go to the current page's Toolbar or Banner.
```

**File Operation Commands**

```shell
c: Create a new file.
d: Download the selected file.
E: Edit the selected file.
f: Show an options menu for the current file.
m: Modify the name or location of the selected file.
r: Remove the selected file.
t: Tag highlighted file.
u: Upload a file to the current directory.
```

**Other Commands**

```shell
?, h: Help.
a: Add the current link to a bookmark file.
c: Send a comment or suggestion to the page owner.
d: Download the current link.
e: Edit the current file.
g: Go to a user-specified URL or file.
G: Edit the current page's URL and jump to it.
i: Show document index.
j: Execute a predefined "short" command.
k: Show keyboard command list.
l: List all link addresses on the current page.
m: Return to the home page.
o: Set options.
p: Output the current page to a file, email, printer, etc.
q: Quit.
/: Search for a string within the current page.
s: Search for a string externally.
n: Find the next occurrence of the search string.
v: View a bookmark file.
V: Go to the history list of visited URLs.
x: Do not use cache.
z: Stop current transfer.
[backspace]: Go back to the previous page (same as V command).
=: Display information about the current page.
\: View source code of the current page.
!: Escape to a shell prompt.
_: Clear all authorization information for the current task.
*: Toggle image link mode.
@: Toggle 8-bit or CJK mode.
[: Toggle pseudo_inlines mode.
]: Send a "HEAD" request for the current page or link.
Ctrl+r: Reload the current page and refresh the screen.
Ctrl+w: Refresh the screen.
Ctrl+u: Delete the input line.
Ctrl+g: Cancel input or transfer.
Ctrl+t: Toggle trace mode.
;: View Lynx's trace logs for the current task.
Ctrl+k: Invoke the Cookie Jar page.
[Number]: Go to the nth link.
```
