# readelf

Used to display information about ELF (Executable and Linkable Format) files.

## Description

The **readelf** command is used to display information about one or more ELF format object files. You can use its options to control which specific information is displayed. `elf-file(s)` represents the files to be examined. It supports both 32-bit and 64-bit ELF files, as well as archives containing ELF files (such as static libraries `lib*.a` created using the `ar` command).

This program provides functionality similar to `objdump`, but it displays more detailed information and does not depend on the BFD library (a GNU project aimed at handling various object file formats through a unified interface). Consequently, `readelf` remains unaffected even if there are bugs in the BFD library.

When running `readelf`, at least one option must be specified, except for `-v` and `-H`.

### ELF File Types

**Three types of ELF files:**

1.  **Relocatable File**: Used with other object files to create an executable or a shared object file (e.g., `myfile.o`, `lib*.a`).
2.  **Executable File**: Used to generate a process image for execution in memory (e.g., compiled executable `a.out`).
3.  **Shared Object File**: Used with other shared object or relocatable files to generate another ELF object file, or with an executable to create a process image (e.g., `lib*.so`).

**Role of ELF Files:**

ELF files participate in program linking (building a program) and execution (running a program). They can be viewed from different perspectives:

1.  **Linking view**: If used for compilation and linking (relocatable files), the compiler and linker see the ELF file as a collection of **sections** described by the Section Header Table. The Program Header Table is optional.
2.  **Execution view**: If used for loading and execution (executable files), the loader sees the ELF file as a collection of **segments** described by the Program Header Table. A segment may contain multiple sections. The Section Header Table is optional.
3.  **Shared view**: Shared files contain both perspectives.

**Overall Composition of ELF Files:**

The ELF file header describes the general information of the file, including system-related, type-related, loading-related, and linking-related details.

*   **System-related**: Includes the Magic Number, hardware, and platform information, which facilitates portability and cross-compilation.
*   **Type-related**: The file type (REL, EXEC, DYN, etc.).
*   **Loading-related**: Program Header Table information.
*   **Linking-related**: Section Header Table information.

### Options

```shell
-a, --all               Display all information (equivalent to -h -l -S -s -r -d -V -A -I).
-h, --file-header       Display the ELF file header.
-l, --program-headers, --segments
                        Display the program headers (segment headers), if any.
-S, --section-headers, --sections
                        Display the section headers, if any.
-g, --section-groups    Display section groups, if any.
-t, --section-details   Display detailed section information (extension of -S).
-s, --syms, --symbols   Display the symbol table entries, if any.
-e, --headers           Display all headers (equivalent to -h -l -S).
-n, --notes             Display note segments (kernel annotations).
-r, --relocs            Display relocation entries.
-u, --unwind           Display unwind information (currently only supports IA64 ELF).
-d, --dynamic           Display the dynamic segment, if any.
-V, --version-info      Display version sections.
-A, --arch-specific     Display architecture-specific information.
-D, --use-dynamic       Use the symbol table in the dynamic segment rather than the symbol section.
-x <number or name>, --hex-dump=<number or name>
                        Dump the contents of a section as hexadecimal.
-w[liaprmfFsoR], --debug-dump[=line,=info,=abbrev,=pubnames,=aranges,=macro,=frames,=frames-interp,=str,=loc,=Ranges]
                        Display the contents of debug sections.
-I, --histogram         Display a histogram of bucket list lengths when showing symbols.
-v, --version           Display the version of readelf.
-H, --help              Display help information.
-W, --wide              Allow output lines to exceed 80 characters.
@file                   Read options from the specified file.
```

### Examples

**1. For executable ELF files:**

Source code (`main.cpp`):

```cpp
#include <iostream>
using std::cout;
using std::endl;
void my_print();

int main(int argc, char *argv[]) 
{ 
        my_print(); 
        cout<<"hello!"<<endl; 
        return 0; 
} 

void my_print() 
{ 
        cout<<"print!"<<endl; 
} 
```

Compilation:

```shell
g++ main.cpp -o main
g++ -g main.cpp -o main.debug
```

In this example, `main.debug` contains debugging information, while `main` is a standard executable.

**2. For library ELF files:**

Source code (`myfile.h` and `myfile.cpp`):

```cpp
// myfile.h
void printInfo();

// myfile.cpp
#include "myfile.h"
#include <iostream>
void printInfo() { std::cout << "hello" << std::endl; }
```

Compilation:

```shell
g++ -c myfile.cpp
g++ -shared -fPIC -o libmy.so myfile.o
ar -r libmy.a myfile.o
```

This generates the object file `myfile.o`, the shared library `libmy.so`, and the static library `libmy.a`.

**Reading the ELF header of an executable:**

```shell
readelf -h main
```

Output highlights:
- **Type**: EXEC (Executable file)
- **Machine**: Intel 80386 (or x86-64 depending on your system)

**Reading the ELF header of an object file:**

```shell
readelf -h myfile.o
```

Output highlights:
- **Type**: REL (Relocatable file)

**Reading the ELF header of a shared library:**

```shell
readelf -h libmy.so
```

Output highlights:
- **Type**: DYN (Shared object file)

**Viewing program headers (segments) of an executable:**

```shell
readelf -l main
```

**Viewing section headers of an executable:**

```shell
readelf -S main
```

This shows sections like `.text` (code), `.data` (initialized data), `.bss` (uninitialized data), and if debugging information is present (like in `main.debug`), you will see `.debug_*` sections.
