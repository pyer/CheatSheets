#PostgreSQL 9 cheat sheet

Connect to a database
```
psql -U [user_name] -d [dbname]
```

Connect and show internal queries
```
psql -U postgres -E
```


Execute a SQL script
```
psql -U [user_name] -d [dbname] -f [file_name.sql]
```

##Backup

to a zipped dump file
```
pg_dump -U postgres -Fc -f [file_name.dump] [dbname]
```

to a script file
```
pg_dump -U postgres -f [file_name.sql] [dbname]
```

a single table
```
pg_dump -U postgres -Fc -a -t [table_name] -f [file_name.dump] [dbname]
```

##Recreate database before restore

```SQL
DROP DATABASE IF EXISTS [dbname];
CREATE DATABASE [dbname] ENCODING 'UTF-8' OWNER [user_name];
\c [dbname]
DROP EXTENSION IF EXISTS plpgsql;
```

##Restore

database from a dump file
```
pg_restore -U [ user_name] -d [dbname] -x -j [threads] [file_name.dump]

```

a single table from a dump file
```
psql -U [user_name] -d [dbname] -c "truncate table historiqueproduitcourant;"
pg_restore -U [user_name] -d [dbname] -t [table_name] [file_name.dump]
```

##Administrator SQL commands

Show running queries
```SQL
SELECT * FROM pg_stat_activity;
```

Cancel a query
```SQL
SELECT pg_cancel_backend(pid);
```

Cancel a query and close connection
```SQL
SELECT pg_terminate_backend(pid);
```

Show postgres settings
```SQL
SELECT name, setting, boot_val, reset_val, unit FROM pg_settings ORDER BY name;
```

Reload configuration
```SQL
SELECT pg_reload_conf();
```

Show last autovacuum
```SQL
SELECT last_autovacuum, last_autoanalyze FROM pg_stat_user_tables
    WHERE last_autovacuum IS NOT NULL
    ORDER BY last_autovacuum DESC;
```

Show size of databases
```SQL
SELECT datname,pg_size_pretty(pg_database_size(datname)) AS size FROM pg_database;
```

Show duplicate records
```SQL
SELECT * FROM table_name t1
    WHERE (SELECT count(*) FROM table_name t2
               WHERE t1.field1=t2.field1 AND t1.field2=t2.field2) > 1;
```

Count duplicate records
```SQL
SELECT field1, field2, count(*) FROM table_name GROUP BY field1, field2 HAVING count(*)>1;
```

Duplicate a table
```SQL
CREATE TABLE target_name AS TABLE table_name;
```

Copy some data from a table to a new one
```SQL
CREATE TABLE target_name AS SELECT field1, field2 FROM table_name WHERE condition;
```

Convert timestamp to epoch (int)
```SQL
SELECT EXTRACT(EPOCH FROM TIMESTAMP '2015-03-01 00:00:00');
```

Convert epoch to timestamp
```SQL
SELECT TO_TIMESTAMP(1425168000);
```

