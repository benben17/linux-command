mysqladmin
===

MySQL server administration client

## Description

The **mysqladmin command** is a client tool for performing administrative tasks on a MySQL server. It can be used to check the server's configuration and current status, create and delete databases, manage users, change passwords, and more.

### Syntax

```shell
mysqladmin [options] [command]
```

### Options

```shell
-h: Hostname or IP address of the MySQL server.
-u: Username used to connect to the MySQL server.
-p: Password used to connect to the MySQL server.
--help: Display help information.
```

### Parameters

Administrative commands: Commands to be executed on the MySQL server.

**Supported commands include:**

```shell
create databasename: Create a new database.
drop databasename: Delete a database and all its tables.
extended-status: Give an extended status message from the server.
flush-hosts: Flush all cached hosts.
flush-logs: Flush all logs.
flush-tables: Flush all tables.
flush-privileges: Reload grant tables (same as reload).
kill id,id,...: Kill mysql threads.
password new_password: Change the old password to a new one.
ping: Check if mysqld is alive.
processlist: Show a list of active threads in the server.
reload: Reload grant tables.
refresh: Flush all tables and close/open log files.
shutdown: Shut down the server.
status: Give a short status message from the server.
variables: Print available variables.
version: Get version information from the server.
```
