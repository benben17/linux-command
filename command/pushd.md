pushd
===

Add a directory to the top of the directory stack.

## Synopsis

```shell
pushd [-n] [+N | -N | dir]
```

## Main Usage

- Adds a directory to the top of the directory stack and switches the current working directory to that directory.

- Rotates the directory stack so that the new top of the stack becomes the current working directory.

- Without arguments, exchanges the top two directories on the stack.

## Options

```shell
-n    Suppresses the normal change of directory when adding directories to the stack, so that only the stack is manipulated.
```

## Parameters

+N (optional): Rotates the stack so that the N-th directory from the left (as shown by the `dirs` command) becomes the top. (Counting from 0)

-N (optional): Rotates the stack so that the N-th directory from the right (as shown by the `dirs` command) becomes the top. (Counting from 0)

dir (optional): The directory to push onto the stack.

## Return Value

Returns success unless an invalid option is provided or an execution error occurs.

## Examples

```shell
# Add a directory to the stack and change the current working directory.
[user2@pc ~]$ dirs
~
[user2@pc ~]$ pushd ~/Desktop
~/Desktop ~
[user2@pc Desktop]$ 
```

```shell
# Add a directory to the stack without changing the current working directory.
[user2@pc ~]$ dirs
~
[user2@pc ~]$ pushd -n ~/Desktop
~ ~/Desktop
[user2@pc ~]$ pushd -n ~/Pictures
~ ~/Pictures ~/Desktop

# Adjust the order of the stack.
[user2@pc ~]$ pushd +1
~/Pictures ~/Desktop ~
[user2@pc ~]$ pushd -1
~/Desktop ~ ~/Pictures
[user2@pc ~]$ pushd
~ ~/Desktop ~/Pictures
```

### Note

1. Bash's directory stack commands include `dirs`, `popd`, and `pushd`.
2. The current directory is always the top of the directory stack.
3. This is a bash builtin command; use the `help` command for related help information.

### Reference Links

- [Behavior of popd and pushd with '-n' option](https://superuser.com/questions/784450/popd-and-pushd-behavior-with-n-option)
