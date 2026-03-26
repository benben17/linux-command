mysqldump
===

MySQL database backup utility

## Description

The **mysqldump command** is a backup utility for MySQL databases. It is used to export databases from a MySQL server as standard SQL statements and save them to a file.

### Syntax

```shell
mysqldump [options]
```

### Options

```shell
--add-drop-table: Add a DROP TABLE statement before each CREATE TABLE statement.
--add-locks: Lock tables when backing up.
--all-databases: Back up all databases on the MySQL server.
--comments: Add comments to the output.
--compact: Compact mode: produces less output.
--complete-insert: Output complete INSERT statements (with column names).
--databases: Specify databases to back up.
--default-character-set: Set the default character set.
--force: Continue backup even if errors occur.
--host: Specify the server where the database is located.
--lock-tables: Lock all tables before starting the backup.
--no-create-db: Do not generate CREATE DATABASE statements.
--no-create-info: Do not generate CREATE TABLE statements.
--password: Password used to connect to the MySQL server.
--port: Port number of the MySQL server.
--user: Username used to connect to the MySQL server.
--skip-lock-tables: Export data without locking tables.
```

### Examples

**Export an entire database:**

```shell
mysqldump -u username -p database_name > export_file.sql
mysqldump -u linuxde -p smgp_apps_linuxde > linuxde.sql
```

**Export a specific table:**

```shell
mysqldump -u username -p database_name table_name > export_file.sql
mysqldump -u linuxde -p smgp_apps_linuxde users > linuxde_users.sql
```

**Export only the database structure:**

```shell
mysqldump -u linuxde -p -d --add-drop-table smgp_apps_linuxde > linuxde_db.sql
```

Note: `-d` means no data, and `--add-drop-table` adds a `DROP TABLE` statement before each `CREATE` statement.

### Troubleshooting

**Lock table failure:**
```
mysqldump: Got error: 1044: "Access denied for user 'appuser'@'1%' to database 'tc_mall'" when doing LOCK TABLES
```
You can use `--skip-lock-tables` to bypass the table locking process during the export phase.
