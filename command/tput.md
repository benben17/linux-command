tput
===

Initialize and manipulate terminal sessions via the terminfo database

## Description

The **tput command** initializes and manipulates your terminal session using the terminfo database. With tput, you can change several terminal features, such as moving or changing the cursor, changing text attributes, and clearing specific areas of the terminal screen.

### What is the terminfo database?

The terminfo database on UNIX systems is used to define the attributes and capabilities of terminals and printers, including the number of rows and columns for each device and the attributes of text sent to that device. Several common programs in UNIX depend on the terminfo database for these attributes and many others, including the vi and emacs editors, as well as the curses and man programs.

Like most commands in UNIX, tput can be used both on the shell command line and in shell scripts. To help you better understand tput, this article starts with the command line and follows with shell script examples.

**Cursor Attributes**

In UNIX shell scripts or on the command line, moving the cursor or changing cursor attributes can be very useful. In some cases, you may need to enter sensitive information (like passwords) or enter information in two different areas on the screen. In such cases, using tput can be helpful.

```shell
tput clear # Clear screen
tput sc # Save current cursor position
tput cup 10 13 # Move cursor to row 10, col 13
tput civis # Make cursor invisible
tput cnorm # Make cursor visible
tput rc # Restore cursor position
exit 0
```

**Moving the Cursor**

tput makes it easy to move the cursor position on various devices. By using the `cup` (cursor position) option in tput, you can move the cursor to any X or Y coordinate across the rows and columns of the device. The top-left corner of the device is (0,0).

To move the cursor to column 5 (X) of row 1 (Y) on the device, simply execute `tput cup 1 5`. Another example is `tput cup 23 45`, which moves the cursor to row 23, column 45.

**Moving the Cursor and Displaying Information**

Another useful cursor positioning trick is to move the cursor, execute a command to display information, and then return to the previous cursor position:

```shell
(tput sc ; tput cup 23 45 ; echo "Input from tput/echo at 23/45" ; tput rc)
```

Let's analyze the subshell command:

```shell
tput sc
```

The current cursor position must be saved first using the `sc` (save cursor position) option.

```shell
tput cup 23 45
```

After saving the cursor position, the cursor coordinates move to (23,45).

```shell
echo "Input from tput/echo at 23/45"
```

Display information to stdout.

```shell
tput rc
```

After displaying this information, the cursor must return to the original position saved with `tput sc`. To return the cursor to its last saved position, include the `rc` (restore cursor position) option.

Note: Since this article first introduces executing tput via the command line, you might find executing commands in your own subshell cleaner than executing each command individually.

**Changing Cursor Attributes**

When displaying data to a device, you often don't want to see the cursor. Making the cursor invisible can make the screen look cleaner as data scrolls. To make the cursor invisible, use the `civis` option (e.g., `tput civis`). After the data is fully displayed, you can make the cursor visible again using the `cnorm` option.

**Text Attributes**

Changing the way text is displayed can draw a user's attention to a group of words in a menu or alert them to something important. You can change text attributes by making text bold, underlining it, changing background and foreground colors, and reversing the color scheme.

To change text color, use the `setb` option (to set background color) and the `setf` option (to set foreground color) along with color numeric values assigned in the terminfo database. Typically, the mapping of values to colors is as follows, though it may vary across UNIX systems:

*   0: Black
*   1: Blue
*   2: Green
*   3: Cyan
*   4: Red
*   5: Magenta
*   6: Yellow
*   7: White

Executing the following example command changes the background color to yellow and the foreground color to red:

```shell
tput setb 6; tput setf 4
```

To reverse the current color scheme, simply execute `tput rev`.

Sometimes, coloring text isn't enough; you may want to catch the user's attention in another way. This can be achieved in two ways: by setting the text to bold or by underlining it.

To change text to bold, use the `bold` option. To start underlining, use the `smul` option. After displaying underlined text, use the `rmul` option.

### Examples

Coloring output string, background, and bold:

```shell
#!/bin/bash
printf $(tput setaf 2; tput bold)'color show\n\n'$(tput sgr0)

for((i=0; i<=7; i++)); do
    echo $(tput setaf $i)"show me the money"$(tput sgr0)
done

printf '\n'$(tput setaf 2; tput setab 0; tput bold)'background color show'$(tput sgr0)'\n\n'

for((i=0,j=7; i<=7; i++,j--)); do
    echo $(tput setaf $i; tput setab $j; tput bold)"show me the money"$(tput sgr0)
done

exit 0
```

Output format control function:

```shell
#!/bin/bash

# $1 str       print string
# $2 color     0-7 set color
# $3 bgcolor   0-7 set background color
# $4 bold      0-1 set bold
# $5 underline 0-1 set underline

function format_output(){
    str=$1
    color=$2
    bgcolor=$3
    bold=$4
    underline=$5
    normal=$(tput sgr0)

    case "$color" in
        0|1|2|3|4|5|6|7)
            setcolor=$(tput setaf $color;) ;;
        *)
            setcolor="" ;;
    esac

    case "$bgcolor" in
        0|1|2|3|4|5|6|7)
            setbgcolor=$(tput setab $bgcolor;) ;;
        *)
            setbgcolor="" ;;
    esac

    if [ "$bold" = "1" ]; then
        setbold=$(tput bold;)
    else
        setbold=""
    fi

    if [ "$underline" = "1" ]; then
        setunderline=$(tput smul;)
    else
        setunderline=""
    fi

    printf "$setcolor$setbgcolor$setbold$setunderline$str$normal\n"
}

format_output "Yesterday Once more" 2 5 1 1

exit 0
```

Cursor attribute example:

```shell
#!/bin/bash
# clear the screen
tput clear
# Move cursor to screen location X,Y (top left is 0,0)
tput cup 3 15
# set a foreground colour using ANSI escape
tput setaf 3
echo "XYX Corp LTD."
tput sgr0
tput cup 5 17
# Set reverse video mode
tput rev
echo "M A I N - M E N U"
tput sgr0
tput cup 7 15
echo "1. User Management"
tput cup 8 15
echo "2. Service Management"
tput cup 9 15
echo "3. Process Management"
tput cup 10 15
echo "4. Backup"
# Set bold mode
tput bold
tput cup 12 15
read -p "Enter your choice [1-4] " choice
tput clear
tput sgr0
tput rc

exit 0
```
