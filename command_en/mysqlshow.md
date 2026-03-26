mysqlshow
===

Display information about MySQL databases, tables, and columns

## Description

The **mysqlshow command** is used to display information about databases, tables, and columns in a MySQL server.

### Syntax

```shell
mysqlshow [options] [database_info]
```

### Options

```shell
-h: Hostname or IP address of the MySQL server.
-u: Username used to connect to the MySQL server.
-p: Password used to connect to the MySQL server.
--count: Show the number of rows in each table.
-k: Show table indexes.
-t: Show table types.
-i: Show extra information about the tables.
```

### Parameters

Database info: Specifies what information to show. This can be a database name, or a database name and a table name, or a database name, table name, and column name.
