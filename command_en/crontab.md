crontab
===

Submit and manage periodic tasks for users

## Description

The **crontab command** is used to submit and manage tasks that need to be executed periodically by users, similar to Scheduled Tasks in Windows. After installing the operating system, this service tool is typically installed and the `crond` process starts automatically. The `crond` process checks for scheduled tasks every minute and executes them automatically if the criteria are met.

### Syntax

```shell
crontab [options] [arguments]
```

### Options

```shell
-e: Edit the current user's crontab entries;
-l: List the current user's crontab entries;
-r: Remove the current user's crontab entries;
-u <username>: Specify the user whose crontab is to be managed.
```

### Arguments

crontab file: Specify a file containing the crontab entries to be loaded.

### Knowledge Extension

Task scheduling in Linux is divided into two categories: **System Task Scheduling** and **User Task Scheduling**.

**System Task Scheduling:** Tasks that the system needs to perform periodically, such as writing cache data to disk or cleaning up logs. The configuration file for system tasks is located at `/etc/crontab`.

The `/etc/crontab` file typically includes the following lines:

```shell
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
51 * * * * root run-parts /etc/cron.hourly
24 7 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

The first four lines configure the environment for `crond` tasks. `SHELL` specifies the shell to use (bash), `PATH` specifies the search path for commands, `MAILTO` specifies that task execution info should be emailed to root (if empty, no email is sent), and `HOME` specifies the home directory for commands or scripts.

**User Task Scheduling:** Tasks that users need to perform periodically, such as data backups or email reminders. Users can use the `crontab` tool to customize their scheduled tasks. All user-defined crontab files are stored in the `/var/spool/cron` directory, with filenames matching the usernames. Relevant permission files include:

```shell
/etc/cron.deny     List of users not allowed to use crontab.
/etc/cron.allow    List of users allowed to use crontab.
/var/spool/cron/   Directory for user crontab files.
```

Meaning of crontab file fields: Each line in a crontab file represents a task. Each line has six fields: the first five are time settings, and the sixth is the command to be executed. The format is as follows:

```shell
minute   hour   day   month   week   command
```

*   **minute:** 0 to 59.
*   **hour:** 0 to 23.
*   **day:** 1 to 31.
*   **month:** 1 to 12.
*   **week:** 0 to 7 (0 or 7 represents Sunday).
*   **command:** The system command or script to execute.

Special characters:
*   **Asterisk (*):** Represents all possible values.
*   **Comma (,):** Used to specify a list of values (e.g., "1,2,5").
*   **Hyphen (-):** Used to specify a range of values (e.g., "2-6").
*   **Forward slash (/):** Used to specify intervals (e.g., "0-23/2" means every two hours). "*/10" in the minute field means every ten minutes.

**crond service commands:**

```shell
/sbin/service crond start    # Start the service
/sbin/service crond stop     # Stop the service
/sbin/service crond restart  # Restart the service
/sbin/service crond reload   # Reload the configuration
```

Check service status:
```shell
service crond status
```

Start the service manually:
```shell
service crond start
```

Check if crontab is set to start on boot:
```shell
ntsysv
# or
chkconfig --level 35 crond on
```

### Examples

Execute command every minute:
```shell
* * * * * command
```

Execute at the 3rd and 15th minute of every hour:
```shell
3,15 * * * * command
```

Execute at the 3rd and 15th minute between 8 AM and 11 AM:
```shell
3,15 8-11 * * * command
```

Execute at the 3rd and 15th minute between 8 AM and 11 AM every two days:
```shell
3,15 8-11 */2 * * command
```

Execute at the 3rd and 15th minute between 8 AM and 11 AM every Monday:
```shell
3,15 8-11 * * 1 command
```

Restart smb at 21:30 every night:
```shell
30 21 * * * /etc/init.d/smb restart
```

Restart smb at 4:45 on the 1st, 10th, and 22nd of every month:
```shell
45 4 1,10,22 * * /etc/init.d/smb restart
```

Restart smb at 1:10 every Saturday and Sunday:
```shell
10 1 * * 6,0 /etc/init.d/smb restart
```

Restart smb every 30 minutes between 18:00 and 23:00 every day:
```shell
0,30 18-23 * * * /etc/init.d/smb restart
```

Restart smb at 11:00 PM every Saturday:
```shell
0 23 * * 6 /etc/init.d/smb restart
```

Restart smb every hour:
```shell
0 */1 * * * /etc/init.d/smb restart
```

Restart smb every hour between 11 PM and 7 AM:
```shell
0 23-7/1 * * * /etc/init.d/smb restart
```

Restart smb at 11 AM on the 4th of the month and from Monday to Wednesday:
```shell
0 11 4 * mon-wed /etc/init.d/smb restart
```

Restart smb at 4 AM on January 1st:
```shell
0 4 1 jan * /etc/init.d/smb restart
```

Execute scripts in `/etc/cron.hourly` every hour:
```shell
01 * * * * root run-parts /etc/cron.hourly
```
观察
