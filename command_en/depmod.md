depmod
===

Analyze loadable module dependencies.

## Description

The **depmod** command generates a module dependency map file. When building an embedded system, this command is needed to generate the corresponding files used by `modprobe`.

### Syntax

```shell
depmod (options)
```

### Options

```shell
-a, --all            Analyze all available modules.
-d, --debug          Execute in debug mode.
-e                   Output symbols that cannot be referenced.
-i                   Do not check the version of the symbol table.
-m <file>, --system-map <file> Use the specified symbol table file.
-s, --system-log     Log errors in the system log (syslog).
-v, --verbose        Show detailed information during execution.
-V, --version        Display version information.
--help               Display help.
```

### Examples

```shell
depmod -b /home/windsome/EMMA3PF-KernelSource-20080626/install_pos -e -F ./boot/System.map -v 2.6.18_pro500-bcm91250-mips2_fp_be -A -a
```

*   `/home/windsome/EMMA3PF-KernelSource-20080626/install_pos` is the storage path for all modules after I ran `make mod_install`.
*   `./boot/System.map` was generated after `make linux` and copied to this directory.
*   `2.6.18_pro500-bcm91250-mips2_fp_be` is the version of the Linux kernel I built.

Example of the Linux compilation process and executing depmod:

```shell
genkernel.sh (at linux-2.6.18_pro500)
#######
export INSTALL_ROOT_EMMA3PF="/home/windsome/EMMA3PF-KernelSource-20080626/install_pos"
export INSTALL_MOD_EMMA3PF="/home/windsome/EMMA3PF-KernelSource-20080626/install_pos"
rm /home/windsome/EMMA3PF-KernelSource-20080626/install_pos/lib -rf
rm /home/windsome/EMMA3PF-KernelSource-20080626/install_pos/boot/* -rf
cd <linux_src_dir>
make
make modules_install
cp vmlinux System.map /home/windsome/EMMA3PF-KernelSource-20080626/install_pos/boot/ -p
cd /home/windsome/EMMA3PF-KernelSource-20080626/install_pos
depmod -b /home/windsome/EMMA3PF-KernelSource-20080626/install_pos -e -F ./boot/System.map -v 2.6.18_pro500-bcm91250-mips2_fp_be -A -a
```

Other usages:

In a Linux desktop system, when you have compiled a new driver, in order to load the module with `modprobe ***`, you first need to copy the module to the `/lib/modules/2.6.31-20-generic` directory, then run `sudo depmod -a` to write the module information into `modules.dep`, `modules.dep.bin`, `modules.alias.bin`, `modules.alias`, and `modules.pcimap` files.

For example, if I compiled a new WiFi driver `r8192se_pci.ko`, I copy it to `/lib/modules/2.6.31-20-generic/wireless`, then go to `/lib/modules/2.6.31-20-generic` and run `depmod -a`. After that, I can run `modprobe r8192se_pci` from any directory.
