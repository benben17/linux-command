ldconfig
===

Dynamic linker run-time bindings management command

## Description

The **ldconfig** command is primarily used to search for shareable dynamic libraries (in the format lib*.so*) in the default directories `/lib` and `/usr/lib`, as well as in the directories listed in the dynamic library configuration file `/etc/ld.so.conf`. It then creates the necessary links and cache files required by the dynamic loader (ld.so). The cache file defaults to `/etc/ld.so.cache`, which stores an ordered list of dynamic library names. To make dynamic libraries shareable across the system, you need to run the `ldconfig` management command, which is located in the `/sbin` directory.

`ldconfig` is typically run at system startup, but it must be run manually whenever a new dynamic library is installed.

### Syntax

```shell
ldconfig [-v|--verbose] [-n] [-N] [-X] [-f CONF] [-C CACHE] [-r ROOT] [-l] [-p|--print-cache] [-c FORMAT] [--format=FORMAT] [-V] -?|--[help|--usage] path... 
```

### Options

```shell
-v, --verbose: Display the directories being scanned, the dynamic libraries found, and the names of the links created.
-n: Only scan directories specified on the command line; do not scan default directories (/lib, /usr/lib) or directories listed in /etc/ld.so.conf.
-N: Do not rebuild the cache file (/etc/ld.so.cache). Unless -X is also specified, ldconfig still updates the links.
-X: Do not update the links. Unless -N is also specified, the cache file is still updated.
-f CONF: Use CONF as the configuration file instead of the default /etc/ld.so.conf.
-C CACHE: Use CACHE as the cache file instead of the default /etc/ld.so.cache.
-r ROOT: Change the root directory to ROOT (implemented using the chroot function). The configuration file /etc/ld.so.conf will then be looked for in ROOT/etc/ld.so.conf.
-l: Expert mode. Normally, ldconfig automatically creates links when searching for dynamic libraries; in expert mode, links must be set manually.
-p, --print-cache: Print the names of all shared libraries currently stored in the cache file.
-c FORMAT, --format=FORMAT: Specify the cache file format: old, new, or compat (the default).
-V: Print the version of ldconfig and exit.
-?, --help, --usage: Display help information and exit.
```

**Notes on ldconfig:**

1. Adding files to `/lib` and `/usr/lib` does not require modifying `/etc/ld.so.conf`, but you must run `ldconfig` afterwards, otherwise the libraries won't be found.
2. When adding libraries to directories other than the two mentioned above, you must modify `/etc/ld.so.conf` and then run `ldconfig`.
3. For example, if you install MySQL to `/usr/local/mysql`, and it has many libraries in `/usr/local/mysql/lib`, you need to add the line `/usr/local/mysql/lib` to `/etc/ld.so.conf` and then run `ldconfig` so the new libraries can be found at runtime.
4. If you want to place libraries outside these directories but don't want to (or can't) modify `/etc/ld.so.conf`, you can export the environment variable `LD_LIBRARY_PATH`. This is generally a temporary solution.
5. `ldconfig` operations are related to program execution, not compilation. During compilation, you still need to use `-L` flags as appropriate.
6. In short, it's best to run `ldconfig` after any changes related to libraries to avoid unexpected results.
7. Files like `libdb-4.3.so` contain library name information in their headers (detectable with the `strings` command). Simply renaming a file to impersonate another library (e.g., `libdb-4.8.so`) will not work. You should specify the library name in the Makefile during compilation.
