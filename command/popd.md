popd
===

Remove directories from the directory stack.

## Synopsis

```shell
popd [-n] [+N | -N]
```

## Main Usage

- Removes directories from the directory stack. If the top directory is removed, the current working directory will switch to the new top directory.

- Without arguments, removes the top of the directory stack.

## Options

```shell
-n    Suppresses the normal change of directory when removing directories from the stack, so that only the stack is manipulated.
```

## Parameters

+N (optional): The N-th directory from the left in the list shown by the `dirs` command without arguments will be removed. (Counting from 0)

-N (optional): The N-th directory from the right in the list shown by the `dirs` command without arguments will be removed. (Counting from 0)


## Return Value

Returns success unless an invalid option is provided or an execution error occurs.

## Examples

```shell
# Add directories to the stack, current working directory remains unchanged.
[user2@pc ~]$ dirs
~
[user2@pc ~]$ pushd -n ~/Desktop
~ ~/Desktop
[user2@pc ~]$ pushd -n ~/Pictures
~ ~/Pictures ~/Desktop
[user2@pc ~]$ pushd -n ~/bin
~ ~/bin ~/Pictures ~/Desktop

# Remove directories from the stack; removing the top directory changes the current working directory:
[user2@pc ~]$ popd -2
~ ~/Pictures ~/Desktop
[user2@pc ~]$ popd +1
~ ~/Desktop
[user2@pc ~]$ popd
~/Desktop
[user2@pc Desktop]$
```

```shell
# Remove directories from the stack; removing the top directory does not change the current working directory:
[user2@pc ~]$ dirs
~
[user2@pc ~]$ pushd -n ~/Desktop
~ ~/Desktop
[user2@pc ~]$ popd -n
~
[user2@pc ~]$ 
```

### Note

1. Bash's directory stack commands include `dirs`, `popd`, and `pushd`.
2. The current directory is always the top of the directory stack.
3. This is a bash builtin command; use the `help` command for related help information.

### Reference Links

- [Behavior of popd and pushd with '-n' option](https://superuser.com/questions/784450/popd-and-pushd-behavior-with-n-option)
