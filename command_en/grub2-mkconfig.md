grub2-mkconfig
===

Generate a `grub.cfg` configuration file.

## Syntax

```shell
Usage: grub2-mkconfig [OPTION]
Generate a GRUB configuration file.

  -o, --output=FILE       Output the generated configuration to FILE [default=stdout]
  -h, --help              Print this message and exit
  -v, --version           Print version information and exit

Report bugs to <bug-grub@gnu.org>.
```

## Examples

Generate a new GRUB configuration file:

```shell
grub2-mkconfig -o /boot/grub2/grub.cfg

# Or using redirection:

grub2-mkconfig > /boot/grub2/grub.cfg
```
