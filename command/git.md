git
===

The world's most advanced distributed version control system.

## Supplemental Information

The **git command** is widely known. Linus Torvalds created the open-source Linux kernel in 1991, which has since grown into the largest server operating system software.

While Linus created Linux, its growth relied on volunteers worldwide. How was this code managed?

Before 2002, volunteers sent source code patches via `diff` to Linus, who merged them manually!

You might wonder why Linus didn't use a version control system. Free systems like CVS and SVN existed, but Linus strongly opposed them because they were slow and required an internet connection. Commercial systems were better but contradicted the open-source spirit of Linux.

By 2002, the codebase was too large for manual management. Linus chose a commercial system called BitKeeper, which the owner, BitMover, allowed the Linux community to use for free.

This arrangement broke down in 2005 when Andrew Tridgell (creator of Samba) attempted to reverse-engineer the BitKeeper protocol. BitMover revoked the free license.

Instead of apologizing, Linus spent two weeks writing his own distributed version control system in C: Git! Within a month, the Linux kernel source was managed by Git.

Git rapidly became the most popular distributed version control system, especially after GitHub launched in 2008, providing free Git hosting for open-source projects like jQuery, PHP, and Ruby.

If BitMover hadn't threatened the Linux community, we might not have the free and powerful Git we use today.

[Git Common Command List](https://github.com/jaywcjlove/handbook/blob/master/other/Git%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4%E6%B8%85%E5%8D%95.md)

### Syntax

```shell
git [--version] [--help] [-C <path>] [-c name=value] [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path] [-p | --paginate | --no-pager] [--no-replace-objects] [--bare] [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>] <command> [<args>]
```

### Options

```shell
add              Add file contents to the index
bisect           Use binary search to find the commit that introduced a bug
branch           List, create, or delete branches
checkout         Check out a branch or paths to the working tree
clone            Clone a repository into a new directory
commit           Record changes to the repository
diff             Show changes between commits, commit and working tree, etc.
fetch            Download objects and refs from another repository
grep             Print lines matching a pattern
init             Create an empty Git repository or reinitialize an existing one
log              Show commit logs
merge            Join two or more development histories together
mv               Move or rename a file, a directory, or a symlink
pull             Fetch from and integrate with another repository or a local branch
push             Update remote refs along with associated objects
rebase           Reapply commits on top of another base tip
reset            Reset current HEAD to the specified state
rm               Remove files from the working tree and from the index
show             Show various types of objects
status           Show the working tree status
tag              Create, list, delete or verify a tag object signed with GPG
```

### Examples

init

```shell
git init # Initialize
```

status

```shell
git status # Get status
```

add

```shell
git add file # . or * adds all
git rm --cached <added_file_to_undo> # Undo git add before commit
git reset head # Alternative to git rm --cached
```

commit

```shell
git commit -m "message"
```

remote

```shell
git remote add origin git@github.com:JSLite/test.git # Add remote origin
```

push

```shell
git push -u origin master # push and set upstream tracking  
git push origin master  
git push -f origin master # Force push
```

clone

```shell
git clone git://github.com/JSLite/JSLite.js.git
git clone git://github.com/JSLite/JSLite.js.git mypro # Clone to custom folder
git clone [user@]example.com:path/to/repo.git/ # SSH syntax
```

`git clone <repository_url> <local_directory>`

```shell
git clone http[s]://example.com/path/to/repo.git/
git clone ssh://example.com/path/to/repo.git/
git clone git://example.com/path/to/repo.git/
git clone /opt/git/project.git 
git clone file:///opt/git/project.git
git clone ftp[s]://example.com/path/to/repo.git/
git clone rsync://example.com/path/to/repo.git/
```

## Configuration

Test account info with `ssh -T git@github.com`.

## Modify Personal Information in Project

```shell
git help config # Get help
git config --global user.name "Your Name"           # Modify global name
git config --global user.email "email@example.com"  # Modify global email
git config --list         # View configuration
```

### Configure Line Endings

Automatically convert CRLF to LF on commit:

```shell
git config --global core.autocrlf input
```

## Common Scenarios

### Create SSH Key

```shell
ssh-keygen -t rsa -C 'email@example.com' # Generate key  
ssh-keygen -t rsa -C "email@example.com" -f ~/.ssh/my_rsa # Specify directory and filename
ssh -T git@github.com # Test connection  
```

### Multi-Account SSH Configuration

**1. Generate named keys**

`ssh-keygen -t rsa -C "email" -f ~/.ssh/jslite_rsa`

**2. Copy key to platform**

`cat ~/.ssh/jslite_rsa.pub`

**3. Modify config file**

```shell
vim ~/.ssh/config
```

```text
Host jslite.github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/jslite_rsa

Host work.github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/work_rsa
```

**4. Test**

```shell
ssh -T git@jslite.github.com  
ssh -T work.github.com        
```

**5. Usage**

```shell
git clone git@jslite.github.com:username/learngit.git
git clone git@work.github.com:username/learngit.git
```

**Note:** If you rename `id_rsa`, add it to the SSH agent:

```shell
ssh-add ~/.ssh/jslite_rsa
ssh-add -l  # List keys
ssh-add -D  # Delete all keys
ssh-add -d ~/.ssh/jslite_rsa # Delete specific key
```

### Password-free Login to Remote Server

```shell
ssh-keygen -t rsa -P '' -f ~/.ssh/server.key
ssh-copy-id -i ~/.ssh/server.key.pub root@192.168.182.112
```

Edit `~/.ssh/config`:

```text
Host my_server
  HostName 192.168.182.112
  User root
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/server.key
```

Login with `ssh my_server`.

### Password-free HTTPS Push

Edit `.git/config`:

```text
[remote "origin"]
- url = https://github.com/username/rep.git
+ url = https://username:password@github.com/username/rep.git
```

### Push to 3 Git Repositories

**1. Add 3 remote URLs**

```shell
git remote add origin https://github.com/JSLite/JSLite.git  
git remote set-url --add origin https://gitlab.com/wang/JSLite.js.git  
git remote set-url --add origin https://oschina.net/wang/JSLite.js.git  
```

**2. Delete a set-url**

```shell
git remote set-url --delete origin https://oschina.net/wang/JSLite.js.git
```

**3. Push code**

```shell
git push origin master
```

**4. Pull code**

Only pulls from the first URL in `origin`.

```shell
git pull origin master   
git pull --all # Fetch all including tags
```

Use `-p` to prune local branches that no longer exist on remote:

```shell
git pull -p
# Equivalent to:
git fetch --prune origin 
```

### Change Remote Repository URL

```shell
git remote remove origin  
git remote add origin git@github.com:username/repo.git  
```

### Revert Remote Records

```shell
git reset --hard HEAD~1 # Revert one commit   
git push -f origin HEAD:master # Sync to remote  
```

### Discard Local Changes

```shell
git reset --hard FETCH_HEAD
```

If error occurs:

```shell
git checkout -b temp 
git checkout master
```

### Simple Discard of Local Changes

```shell
git reset --hard # Discard staged and unstaged changes
git checkout . # Revert all changes, but don't delete new files
git clean -xdf # Delete untracked files
```

Using stash:

```shell
git stash && git stash drop 
```

### Revert to a specific commit

```shell
git revert HEAD~1 # Reverts the commit and creates a new commit
git push
```

### Reset to a version

```shell
git reset --hard <hash>
# --hard discards all local changes
# --soft keeps local changes
```

### Create a Blank Branch

```shell
git checkout --orphan gh-pages
git rm -rf .
```

### Squash Multiple Commits

```shell
git rebase -i HEAD~4 
# Change 'pick' to 'squash' (or 's') for commits to be squashed
git push -f origin master
```

### Modify Historical Commit Info

```shell
git commit --amend # Modify last commit
git rebase -i HEAD~3 # Modify last 3 commits
# Change 'pick' to 'edit'
# Then:
git commit --amend
git rebase --continue
git push -f origin master
```

### Sync a Fork

```shell
git remote add upstream https://github.com/original_owner/repo.git
git fetch upstream
git checkout master
git merge upstream/master
```

### Batch Modify Author Name and Email

```shell
git filter-branch -f --env-filter '
OLD_EMAIL="old@example.com"
CORRECT_NAME="New Name"
CORRECT_EMAIL="new@example.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

Force push:

```shell
git push --force --tags origin 'refs/heads/*'
```

### View File History

```shell
git log --pretty=oneline filename  
git show <hash>   
git blame filename     
```

### Git Aliases

```shell
git config --global alias.st status
git config --global alias.br branch
git config --global alias.co checkout
git config --global alias.ci commit
```

### Submodules

```shell
git clone --recurse-submodules <url>
# Or manually:
git submodule add <url> <path>
git submodule init
git submodule update
```

Update all submodules:

```shell
git submodule foreach git pull origin master
```

### Logs

```shell
git log --pretty=oneline
git log --graph --oneline --abbrev-commit
git reflog # History of all actions
```

### References

- [Official Git Website](http://git-scm.com/)
- [GitHub: Learn Git in 15 Minutes](https://try.github.io)
- [Pro Git Book](http://git-scm.com/book/en/v2)
