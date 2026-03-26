chkconfig
===

Check or set various system services

## Description

The **chkconfig command** checks and sets various system services. This is a program developed by Red Hat under the GPL rules. It can query which system services will be executed in each runlevel of the operating system, including various resident services. Note that `chkconfig` does not immediately stop or start a service; it simply changes the symbolic links.

### Syntax

```shell
chkconfig [options]
```

### Options

```shell
--add: Add the specified system service so that chkconfig can manage it, and add relevant data to the system startup description files.
--del: Remove the specified system service from chkconfig management and delete relevant data from the system startup description files.
--level <runlevels>: Specify the runlevels at which the system service should be started or stopped.
```
Default runlevels used by RHS:

* 0: Halt
* 1: Single-user mode
* 2: Multi-user mode without networking
* 3: Full multi-user mode with networking
* 4: Unused
* 5: X11 (Multi-user mode with networking and X Window system)
* 6: Reboot

Detailed explanation of each runlevel:

* 0: Halt, the machine is shut down.
* 1: Single-user mode, similar to Safe Mode in Win9x.
* 2: Multi-user mode, but without NFS support.
* 3: Full multi-user mode, the standard runlevel.
* 4: Generally not used, can be used for special purposes in some cases (e.g., laptop power management).
* 5: X11, enters the X Window system.
* 6: Reboot, running `init 6` will reboot the machine.

Note that the `--level` option can specify the runlevels to check, not necessarily the current runlevel. For each runlevel, there can be only one start script or stop script. When switching runlevels, `init` will not restart already started services, nor will it stop already stopped services.

Runlevel files:

Each service managed by `chkconfig` needs to have two or more lines of comments added to its script in `init.d`. The first line tells `chkconfig` the default runlevels to start in, as well as the start and stop priorities. If a service is not started in any runlevel by default, use `-` instead of runlevels. The second line describes the service and can be continued across multiple lines using `\`.

For example, `random.init` contains three lines:

```shell
# chkconfig: 2345 20 80
# description: Saves and restores system entropy pool for \
# higher quality random number generation.
```

### Examples

```shell
chkconfig --list             # List all system services.
chkconfig --add httpd        # Add the httpd service.
chkconfig --del httpd        # Delete the httpd service.
chkconfig --level httpd 2345 on        # Set httpd to "on" in runlevels 2, 3, 4, and 5.
chkconfig --list               # List the startup status of all system services.
chkconfig --list mysqld        # List the settings for the mysqld service.
chkconfig --level 35 mysqld on # Set mysqld to start in runlevels 3 and 5.
chkconfig mysqld on            # Set mysqld to "on" in runlevels 2, 3, 4, and 5.

chkconfig --level redis 2345 on # Set redis to "on" in runlevels 2, 3, 4, and 5.
```

How to add a service:

1. The service script must be stored in the `/etc/init.d/` directory.
2. `chkconfig --add servicename` adds the service to the `chkconfig` list, creating K/S entries in `/etc/rc.d/rcN.d`.
3. `chkconfig --level 35 mysqld on` modifies the default startup levels of the service.
