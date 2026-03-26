mail
===

Send and receive emails from the command line

## Description

The **mail command** is a utility for sending and receiving emails via the command line. While its interface may not be as user-friendly as `elm` or `pine`, it provides comprehensive functionality.

### Syntax

```shell
mail [OPTION]... [ADDRESS]
```

### Options

```shell
-b <address>: Specify blind carbon copy (BCC) recipient.
-c <address>: Specify carbon copy (CC) recipient.
-f <mailbox>: Read emails from the specified mailbox file.
-i: Ignore terminal interrupt signals.
-I: Enable interactive mode.
-n: Do not read the system-wide mail.rc file.
-N: Do not display message headers when reading mail.
-s <subject>: Specify the subject of the email.
-u <user>: Read the mailbox of the specified user.
-v: Enable verbose mode to display detailed delivery information.
```

### Parameters

Email Address: The recipient's email address.

### Examples

**Using the Shell as an Editor**

```shell
mail -s "Hello from shell" admin@example.com
This is the content of the mail.
Welcome to example.com.
```

The first line is the command, where `-s` specifies the subject. After pressing Enter, you can type the body of the email. Press **CTRL+D** to finish and send. You will be prompted for a "Cc" address; press Enter to skip.

**Using a Pipe to Send Mail**

```shell
echo "This is the content of the mail." | mail -s "Hello via pipe" admin@example.com
```

This completes the email sending in a single line using a pipe.

**Sending a File as the Email Body**

```shell
mail -s "Hello via file" admin@example.com < mail.txt
```

This sends the content of `mail.txt` as the body of the email.

**Configuring Sender via Sendmail Options**

Since `mail` typically calls `sendmail` for delivery, you can pass parameters to `sendmail`. For example, to specify a sender:

```shell
mail -s "Hello with sender" admin@example.com -- -f user@example.com < mail.txt
```

The `--` separates `mail` options from `sendmail` options, where `-f` sets the envelope sender address.

**Sending Attachments**

To send attachments, you typically use `uuencode` (part of the `sharutils` package) to encode binary files for transmission:

```shell
uuencode test.txt test.txt | mail -s "See the attachment" admin@example.com < mail.txt
```

This sends `test.txt` as an attachment. The first argument to `uuencode` is the source file, and the second is the filename as it will appear in the email.

Note: Ensure that `sendmail` or an equivalent MTA is installed and configured on your system for `mail` to function correctly.
