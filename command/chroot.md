chroot
===

Run a command or interactive shell with a special root directory

## Description

The **chroot command** is used to run a command with a specified root directory. "chroot" stands for "change root directory." In Linux systems, the default directory structure starts from `/`, the root. After using `chroot`, the system directory structure will use the specified location as the `/` position.

After executing the `chroot` command, the directories and files perceived by the system will no longer be under the old system root, but rather the new root directory structure. This brings several benefits:

**Increased system security by restricting user privileges:**

After `chroot`, the root directory structure and files of the old system cannot be accessed under the new root, which enhances system security. This is often used before login to prevent users from accessing specific files.

**Creating an isolated system directory structure for easier development:**

With `chroot`, the system reads directories and files under the new root, which is independent of the original system root. This environment can be used to test software static compilation and for independent development tasks unrelated to the main system.

**Switching the system root location for booting and system rescue:**

The most prominent use of `chroot` is during the initial boot process. It switches the system root from the initial RAM disk (initrd) to the actual root to execute the real `init`. Additionally, when system issues occur, `chroot` can be used to switch to a temporary system for repairs.

### Syntax

```shell
chroot [options] [arguments]
```

### Options

```shell
--help: Online help;
--version: Display version information.
```

### Arguments

*   Directory: Specify the new root directory;
*   Command: Specify the command to execute.

### Examples

**Use `target` as the root directory (running `/bin/sh` within it):**

```shell
chroot target /bin/sh
```

Here, `target` is the installation path of `busybox`, which resembles a filesystem containing many tools. This will enter a shell environment where `target` is the root. Running `exit` or pressing `Ctrl+D` will exit this shell and return to the original environment.

Note:
*   Root privileges are required.
*   If you run `chroot target` without a command, it defaults to looking for `target/bin/bash` or `/bin/sh`.

**Use `target` as the root directory (running `/bin/ls` within it):**

```shell
chroot target /bin/ls
```

In this case, it runs the `ls` command from within `target` (not the host's `/bin/ls`) and then immediately returns to the host environment.

Note: If you compile a program locally (e.g., `a.out`) and copy it to `target/bin/`, it might not run if it depends on dynamic libraries. You need to use `ldd` to check the required libraries for `a.out` and copy those libraries to the corresponding paths under the new root.

**Running a custom-compiled program with `chroot`:**

Prepare the chroot root directory:

```shell
mkdir newRoot
```

Compile your program:

```shell
gcc main.c
```

Assume `main.c` generates `a.out`, which prints "hello."

Check the required libraries:

```shell
ldd a.out
```

Example output:

```shell
linux-gate.so.1 => (0xb8034000)
libc.so.6 => /lib/tls/i686/cmov/libc.so.6 (0xb7eab000)
/lib/ld-linux.so.2 (0xb801a000)
```

Copy the program and its required libraries to the new root directory:

```shell
cp a.out newRoot
mkdir newRoot/lib
cp /lib/tls/i686/cmov/libc.so.6 newRoot/lib
cp /lib/ld-linux.so.2 newRoot/lib
```

The contents of `newRoot` will look like this:

```shell
a.out lib/
```

Run your program using `chroot`:

```shell
su
chroot newRoot /a.out
```

Now `a.out` will run correctly. Because `a.out` uses dynamic libraries, they must be copied to `newRoot`. If there were no library dependencies, copying `a.out` alone would suffice. For example, a statically compiled `busybox` in `/bin/busybox` does not rely on other libraries.
