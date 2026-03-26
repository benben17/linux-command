rsync
===

Remote data synchronization tool.

## Description

The **rsync command** is a remote data synchronization tool that can quickly synchronize files between multiple hosts over LAN/WAN. `rsync` uses the so-called "rsync algorithm" to achieve synchronization between local and remote hosts. This algorithm only transmits the differing parts of two files rather than transmitting the entire file every time, making it significantly faster. `rsync` is a very powerful tool with many functional options.

### Syntax

```shell
rsync [OPTION]... SRC DEST
rsync [OPTION]... SRC [USER@]host:DEST
rsync [OPTION]... [USER@]HOST:SRC DEST
rsync [OPTION]... [USER@]HOST::SRC DEST
rsync [OPTION]... SRC [USER@]HOST::DEST
rsync [OPTION]... rsync://[USER@]HOST[:PORT]/SRC [DEST]
```

Corresponding to the six command formats above, `rsync` has six different working modes:

1.  Copy local files. This mode is activated when neither the SRC nor the DEST path contains a single colon ":" separator. E.g., `rsync -a /data /backup`
2.  Use a remote shell program (e.g., rsh, ssh) to copy local content to a remote machine. This mode is activated when the DST path contains a single colon ":" separator. E.g., `rsync -avz *.c foo:src`
3.  Use a remote shell program (e.g., rsh, ssh) to copy remote content to the local machine. This mode is activated when the SRC path contains a single colon ":" separator. E.g., `rsync -avz foo:src/bar /data`
4.  Copy files from a remote rsync server to the local machine. This mode is activated when the SRC path contains a "::" separator. E.g., `rsync -av root@192.168.78.192::www /databack`
5.  Copy files from the local machine to a remote rsync server. This mode is activated when the DST path contains a "::" separator. E.g., `rsync -av /databack root@192.168.78.192::www`
6.  List files on a remote machine. This is similar to an rsync transfer, but the local machine information is omitted. E.g., `rsync -v rsync://192.168.78.192/www`

### Options

```shell
-v, --verbose: Verbose output.
-q, --quiet: Suppress non-error messages.
-c, --checksum: Skip based on checksum, not mod-time & size.
-a, --archive: Archive mode; equals -rlptgoD (recursive, preserves symlinks, permissions, times, group, owner, and device files).
-r, --recursive: Recurse into directories.
-R, --relative: Use relative path names.
-b, --backup: Make backups (see --suffix & --backup-dir).
--backup-dir: Make backups into hierarchy based in DIR.
-suffix=SUFFIX: Backup suffix (default ~ unless specified).
-u, --update: Skip files that are newer on the receiver.
-l, --links: Copy symlinks as symlinks.
-L, --copy-links: Transform symlink into referent file/dir.
--copy-unsafe-links: Only "unsafe" symlinks are transformed.
--safe-links: Ignore symlinks that point outside the tree.
-H, --hard-links: Preserve hard links.
-p, --perms: Preserve permissions.
-o, --owner: Preserve owner (root only).
-g, --group: Preserve group.
-D, --devices: Preserve device files (root only).
-t, --times: Preserve modification times.
-S, --sparse: Handle sparse files efficiently.
-n, --dry-run: Show what would have been transferred.
-w, --whole-file: Copy files whole (without delta-xfer algorithm).
-x, --one-file-system: Don't cross filesystem boundaries.
-B, --block-size=SIZE: Force a fixed checksum block-size.
-e, --rsh=COMMAND: Specify the remote shell to use.
--rsync-path=PROGRAM: Specify the rsync to run on the remote machine.
-C, --cvs-exclude: Auto-ignore files in the same way CVS does.
--existing: Skip creating new files on receiver.
--delete: Delete extraneous files from dest dirs.
--delete-excluded: Also delete excluded files from dest dirs.
--delete-after: Receiver deletes after transfer, not before.
--ignore-errors: Delete even if there are I/O errors.
--max-delete=NUM: Don't delete more than NUM files.
--partial: Keep partially transferred files.
--force: Force deletion of dirs even if not empty.
--numeric-ids: Don't map uid/gid values by user/group name.
--timeout=SECONDS: Set I/O timeout in seconds.
-I, --ignore-times: Don't skip files that match size and time.
--size-only: Skip files that match in size.
--modify-window=NUM: Compare mod-times with reduced accuracy.
-T --temp-dir=DIR: Create temporary files in directory DIR.
--compare-dest=DIR: Also compare destination files relative to DIR.
-P: Same as --partial --progress.
--progress: Show progress during transfer.
-z, --compress: Compress file data during the transfer.
--exclude=PATTERN: Exclude files matching PATTERN.
--include=PATTERN: Don't exclude files matching PATTERN.
--exclude-from=FILE: Read exclude patterns from FILE.
--include-from=FILE: Read include patterns from FILE.
--version: Print version number.
--address=ADDRESS: Bind to the specified address.
--config=FILE: Specify alternate rsyncd.conf file.
--port=PORT: Specify alternate rsyncd port number.
--blocking-io: Use blocking I/O for the remote shell.
-stats: Give some file-transfer stats.
--log-format=FORMAT: Log updates using specified format.
--password-file=FILE: Read daemon-access password from FILE.
--bwlimit=RATE: Limit socket I/O bandwidth.
-h, --help: Show help.
```

### Examples

**SSH Method**

First, start the SSH service on the server:

```shell
service sshd start
Starting sshd: [ OK ]
```

**Using rsync for synchronization**

Next, you can use the `rsync` command on the client to back up data from the server. The SSH method uses system users for the backup:

```shell
rsync -vzrtopg --progress -e ssh --delete work@172.16.78.192:/www/* /databack/experiment/rsync
work@172.16.78.192's password:
receiving file list ...
5 files to consider
test/
a
0 100% 0.00kB/s 527:35:41 (1, 20.0% of 5)
b
67 100% 65.43kB/s 0:00:00 (2, 40.0% of 5)
c
0 100% 0.00kB/s 527:35:41 (3, 60.0% of 5)
dd
100663296 100% 42.22MB/s 0:00:02 (4, 80.0% of 5)
sent 96 bytes received 98190 bytes 11563.06 bytes/sec
total size is 100663363 speedup is 1024.19
```

The above information describes the entire backup process and the total size of the backed-up data.

**Daemon Method**

Start the rsync service by editing the `/etc/xinetd.d/rsync` file, changing `disable=yes` to `disable=no`, and restarting the xinetd service:

```shell
vi /etc/xinetd.d/rsync

# default: off
# description: The rsync server is a good addition to an ftp server, as it \
# allows crc checksumming etc.
service rsync {
disable = no
socket_type = stream
wait = no
user = root
server = /usr/bin/rsync
server_args = --daemon
log_on_failure += USERID
}
```

```shell
/etc/init.d/xinetd restart
Stopping xinetd: [ OK ]
Starting xinetd: [ OK ]
```

Create the configuration file. After the `rsync` program is installed, the main configuration file is not created automatically. You need to create `/etc/rsyncd.conf` manually and insert content like the following:

```shell
vi /etc/rsyncd.conf

uid=root
gid=root
max connections=4
log file=/var/log/rsyncd.log
pid file=/var/run/rsyncd.pid
lock file=/var/run/rsyncd.lock
secrets file=/etc/rsyncd.passwd
hosts deny=172.16.78.0/22

[www]
comment= backup web
path=/www
read only = no
exclude=test
auth users=work
```

Create a password file. This method does not use system users for client authentication, so a password file is needed in the format "username:password". The username and password can be anything; it's best not to match system accounts. Set the password file permissions to 600.

```shell
echo "work:abc123" > /etc/rsyncd.passwd
chmod 600 /etc/rsyncd.passwd
```

Backup: Now you can back up the data:

```shell
rsync -avz --progress --delete work@172.16.78.192::www /databack/experiment/rsync

Password:
receiving file list ...
6 files to consider
./ files...
a
0 100% 0.00kB/s 528:20:41 (1, 50.0% of 6)
b
67 100% 65.43kB/s 0:00:00 (2, 66.7% of 6)
c
0 100% 0.00kB/s 528:20:41 (3, 83.3% of 6)
dd
100663296 100% 37.49MB/s 0:00:02 (4, 100.0% of 6)
sent 172 bytes received 98276 bytes 17899.64 bytes/sec
total size is 150995011 speedup is 1533.75
```

Restore: When data on the server has issues, you can restore it from the client, provided the server allows write access:

```shell
rsync -avz --progress /databack/experiment/rsync/ work@172.16.78.192::www

Password:
building file list ...
6 files to consider
./
a
b
67 100% 0.00kB/s 0:00:00 (2, 66.7% of 6)
c
sent 258 bytes received 76 bytes 95.43 bytes/sec
total size is 150995011 speedup is 452080.87
```

**Synchronize Source Directory to Target Directory**

```shell
$ rsync -r source destination
```

The `-r` flag means recursive, including subdirectories. Note that `-r` is required, otherwise `rsync` will not succeed. `source` is the source directory, and `destination` is the target directory.

**Synchronize Multiple Files or Directories**

```shell
$ rsync -r source1 source2 destination
```

Both `source1` and `source2` will be synchronized into the `destination` directory.

**Synchronize Metadata**

The `-a` parameter can replace `-r`. In addition to recursive synchronization, it also synchronizes metadata (such as modification times, permissions, etc.). Since `rsync` uses file size and modification time by default to determine if a file needs updating, `-a` is more useful than `-r`. This is the common usage:

```shell
$ rsync -a source destination
```

If `destination` does not exist, `rsync` will create it automatically. After executing the above command, the source directory `source` is copied in its entirety under the target directory `destination`, resulting in a `destination/source` structure.

If you only want to synchronize the *contents* of the `source` directory into `destination`, add a slash after the source directory:

```shell
$ rsync -a source/ destination
```

After this, the contents of the `source` directory are copied directly into `destination`, without creating a `source` subdirectory.

**Simulate Execution Results (Dry Run)**

If you are unsure of the outcome, use `-n` or `--dry-run` to simulate the execution:

```shell
$ rsync -anv source/ destination
```

The `-n` parameter simulates the command without actually executing it. The `-v` parameter outputs the results to the terminal.

**Make Target Directory a Mirror Copy of Source**

By default, `rsync` only ensures that all content from the source is copied to the destination. It doesn't delete files from the destination that are not in the source. To make the destination a mirror copy, use the `--delete` parameter:

```shell
$ rsync -av --delete source/ destination
```

**Exclude Files**

To exclude certain files or directories during synchronization, use the `--exclude` parameter:

```shell
$ rsync -av --exclude='*.txt' source/ destination
# or
$ rsync -av --exclude '*.txt' source/ destination
```

Note that `rsync` synchronizes hidden files (those starting with a dot). To exclude hidden files, use `--exclude=".*"`.

To exclude all files within a directory but keep the directory itself:

```shell
$ rsync -av --exclude 'dir1/*' source/ destination
```

For multiple exclusion patterns, use multiple `--exclude` parameters or Bash brace expansion:

```shell
$ rsync -av --exclude={'file1.txt','dir1/*'} source/ destination
```

If there are many patterns, write them in a file (one per line) and use `--exclude-from`:

```shell
$ rsync -av --exclude-from='exclude-file.txt' source/ destination
```

**Include Specific File Patterns**

The `--include` parameter specifies file patterns that *must* be synchronized, often used in conjunction with `--exclude`:

```shell
$ rsync -av --include="*.txt" --exclude='*' source/ destination
```

This excludes all files except those ending in `.txt`.

**Specify the Remote Shell**

The remote shell is used to establish a connection between local and remote hosts. It is not the shell (like bash/zsh) that executes scripts.

The `-e` option specifies the remote shell to use (default is ssh), such as rsh, socat, or a custom script:

```shell
$ rsync -av -e rsh /tmp/src/ user@host:/tmp/dest/
```

The `-e` option can also include parameters for the remote shell. If you need to specify an SSH user, you must use `ssh -l user`:

```shell
$ rsync -av -e "ssh -l root -p 9000" /tmp/src/ user@192.168.56.12:/tmp/dest/
```

**Transfer via SSH-Encrypted Daemon**

When using daemon syntax (`host::module` or `rsync://host/module`), the default is to connect directly to the remote rsync daemon over TCP port 873 in plain text.

```shell
$ rsync -av /tmp/src/ testuser@192.168.56.12::max
```

By adding `-e ssh`, rsync logs in via SSH and starts a temporary, single-use daemon within the SSH session. This encrypts the daemon transfer via SSH. The temporary daemon does not listen on any TCP ports.

```shell
# Uses current Linux user as SSH user; will prompt for rsync user password for module 'max'
$ rsync -av -e ssh /tmp/src/ 192.168.56.12::max
```

It's recommended to explicitly specify the SSH user with `ssh -l user` and the rsync user in the daemon syntax to avoid confusion:

```shell
# Uses 'user' for SSH connection and 'testuser' as rsync user
$ rsync -av -e "ssh -l user" /tmp/src/ testuser@192.168.56.12::max
```

In this mode, the remote rsync process runs as the SSH user and looks for `rsyncd.conf` in that user's home directory. If not found, it errors (unless the SSH user is root, in which case it reads `/etc/rsyncd.conf`).

You can create a `rsyncd.conf` in the SSH user's home directory with content like:

```
[max]
    path = /tmp/dest
    read only = no
    auth users = testuser
    secrets file = /home/user/rsyncd.secrets
```

Ensure the configuration does not use options requiring root (like `uid`, `gid`, `chroot`). Create the secrets file `/home/user/rsyncd.secrets` (e.g., `testuser:123123`) and set its permissions to 600.

**Transfer via SSH Tunnel to Daemon**

Another way is to use an SSH tunnel to encrypt communication with a normal daemon.

If the remote daemon is listening on `127.0.0.1:873`, you can map that port to your local machine via SSH:

```shell
$ ssh -L 8873:127.0.0.1:873 user@192.168.56.12
```

Then use the local port for synchronization (traffic is encrypted through the SSH tunnel):

```shell
$ rsync -av /tmp/src/ testuser@127.0.0.1::max --port=8873
```
