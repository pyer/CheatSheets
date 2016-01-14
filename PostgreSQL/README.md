#PostgreSQL 9 cheat sheet


##psql interactive terminal
Type "help" for help.

####Connect to a database
`psql -U [user_name] -d [dbname]`

####Connect and show internal queries
`psql -U postgres -E`


##Execute a SQL script
`psql -U [user_name] -d [dbname] -f [file_name.sql]`


##Backup

####to a zipped dump file
`pg_dump -U postgres -Fc -f [file_name.dump] [dbname]`

####to a script file
`pg_dump -U postgres -f [file_name.sql] [dbname]`


##Restore

####database from a dump file
```
dropdb     -U [user_name] --if-exists [dbname]
createdb   -U [user_name] -E 'UTF-8' [dbname]
psql       -U [user_name] -d [dbname] -c "DROP EXTENSION IF EXISTS plpgsql;"
pg_restore -U [user_name] -d [dbname] -x -j [threads] [file_name.dump]
```

####only one table from a dump file
```
pg_restore -U [user_name] -d [dbname] --table=table_name [file_name.dump]
```


##SQL commands

####Create a database
```SQL
CREATE DATABASE [dbname] ENCODING 'UTF-8' owner [user_name];
```

####Drop a database
```SQL
DROP DATABASE [dbname];
```

####Running queries
```SQL
SELECT * FROM pg_stat_activity;
```

####Cancel query
```SQL
SELECT pg_cancel_backend(pid);
```

####Cancel query and close connection
```SQL
SELECT pg_terminate_backend(pid);
```

####Postgres settings
```SQL
SELECT name, setting, boot_val, reset_val, unit FROM pg_settings ORDER BY name;
```

####Last autovacuum
```SQL
SELECT last_autovacuum, last_autoanalyze FROM pg_stat_user_tables
    WHERE last_autovacuum IS NOT NULL
    ORDER BY last_autovacuum DESC;
```
