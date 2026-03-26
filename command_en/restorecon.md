restorecon
===

Restore file security context.

## Description

The **restorecon command** is used to restore SELinux file attributes, i.e., restoring the security context of files.

### Syntax

```shell
restorecon [-iFnrRv] [-e excludedir ] [-o filename ] [-f filename | pathname...]
```

### Options

```shell
-i: Ignore non-existent files.
-f: infilename; specifies a file containing a list of files to be processed.
-e: directory; excludes the specified directory.
-R/-r: Processes directories recursively.
-n: Do not change file labels.
-o/outfilename: Saves the list of files with incorrect labels to outfilename.
-v: Displays the progress on the screen.
-F: Forces restoration of the file security context.
```

### Examples

Suppose CentOS has Apache installed, and the default web home directory is `/var/www/html`. We often encounter a problem where a web page file is created in another directory and then moved to the default web directory `/var/www/html` using `mv`. However, the file cannot be opened in a browser. This is likely because the SELinux configuration of the file is inherited from its original directory, which differs from `/var/www/html`. When using `mv`, the SELinux configuration is moved along with the file, leading to the inability to open the page. See the following example:

Using CentOS as an example, if Apache is not installed by default, ensure a network connection and use the following command to install it:

```shell
[root@jsdig.com ~]# yum install httpd
# Create a new html file in root's home directory
[root@jsdig.com ~]# pwd
/root

[root@jsdig.com ~]# vi index.html

# Enter some text, save and exit
welcome to www.jsdig.com

# Move this file to the default web directory
[root@jsdig.com ~]# mv index.html /var/www/html/

#
# At this point, entering 127.0.0.1/index.html in the Firefox browser shows it cannot be opened.
# Checking the SELinux log file reveals the following error message. It is clear that
# the httpd process was blocked by SELinux when accessing index.html in the web home directory.
# The reason is that the SELinux configuration is incorrect.
# The correct SELinux configuration should be the part after "scontext=".
# However, the SELinux configuration for index.html is the part after "tcontext=".
# From the third part of "tcontext=", "admin_home_t", it is evident that this file's
# SELinux configuration is from the root user's home directory.
#
type=AVC msg=audit(1378974214.610:465): avc:  denied  { open } for  pid=2359 comm="httpd" path="/var/www/html/index.html" dev="sda1" ino=1317685 scontext=system_u:system_r:httpd_t:s0 tcontext=unconfined_u:object_r:admin_home_t:s0 tclass=file
```

Using `ls -Z` also shows that the SELinux information of the file and directory do not match:

```shell
[root@jsdig.com html]# ls -Z /var/www/html/
.... unconfined_u:object_r:admin_home_t:s0 index.html

[root@jsdig.com html]# ls -Zd /var/www/html/
.... system_u:object_r:httpd_sys_content_t:s0 /var/www/html/
```

Use `restorecon` to restore the SELinux configuration of all files in the web home directory (if the target is a directory, you can add the `-R` parameter for recursion):

```shell
[root@jsdig.com html]# restorecon -R /var/www/html/
```
