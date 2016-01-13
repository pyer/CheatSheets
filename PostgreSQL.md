#PostgreSQL 9 cheat sheet


##Backup

####to a zipped file
`pg_dump -U postgres -Fc -f __FILE_NAME__.dump __DBNAME__`

####to a script file
`pg_dump -U postgres -f __FILE_NAME__.sql __DBNAME__`


##Restore

####a dump file
```
dropdb -U __USER_NAME__ --if-exists __DBNAME__
createdb -U __USER_NAME__ -E 'UTF-8' __DBNAME__
psql -U __USER_NAME__ -d __DBNAME__ -c "DROP EXTENSION IF EXISTS plpgsql;"
pg_restore -U __USER_NAME__ -j THREADS --dbname=__DBNAME__ __FILE_NAME__.dump
```

####a dump file, if __USER_NAME__ cannot create a database
```
createdb -U postgres -O __USER_NAME__ -E 'UTF-8' __DBNAME__
pg_restore -U postgres -j THREADS -O --role=__USER_NAME__ --dbname=__DBNAME__ --table=table_name __FILE_NAME__.dump
```

####only one table from a dump file
`pg_restore -U __USER_NAME__ --dbname=__DBNAME__ --table=table_name __FILE_NAME__.dump`

####a SQL script (same as executing any SQL script)
`psql -U __USER_NAME__ -d __DBNAME__ -f __FILE_NAME__.sql`


##Database administration

####Create a database
`psql -U __USER_NAME__ -c "CREATE DATABASE __DBNAME__ ENCODING 'UTF-8';"`

####Create a database with Postgres tool
`createdb -U __USER_NAME__ -E 'UTF-8' __DBNAME__`

####Drop a database
`psql -U __USER_NAME__ -c "DROP DATABASE __DBNAME__;"`

####Drop a database with Postgres tool
`dropdb -U __USER_NAME__ __DBNAME__`


##Monitoring commands


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
