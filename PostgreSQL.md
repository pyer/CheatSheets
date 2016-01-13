#PostgreSQL 9 cheat sheet


##Backup

####to a zipped file
`pg_dump -U postgres -Fc -f file_name.dump database_name`

####to a script file
`pg_dump -U postgres -f file_name.sql database_name`


##Restore

####a dump file
`dropdb -U user_name --if-exists database_name`

`createdb -U user_name -E 'UTF-8' database_name`

`psql -U user_name -d database_name -c "DROP EXTENSION IF EXISTS plpgsql;"`

`pg_restore -U user_name -j number_of_threads --dbname=database_name file_name.dump`

####a dump file, if user_name cannot create a database
`createdb -U postgres -O user_name -E 'UTF-8' database_name`

`pg_restore -U postgres -j number_of_threads -O --role=user_name --dbname=database_name --table=table_name file_name.dump`

####only one table from a dump file
`pg_restore -U user_name --dbname=database_name --table=table_name file_name.dump`

####a SQL script (same as executing any SQL script)
`psql -U user_name -d database_name -f file_name.sql`


##Database administration

####Create a database
`psql -U user_name -c "CREATE DATABASE database_name ENCODING 'UTF-8';"`

####Create a database with Postgres tool
`createdb -U user_name -E 'UTF-8' database_name`

####Drop a database
`psql -U user_name -c "DROP DATABASE database_name;"`

####Drop a database with Postgres tool
`dropdb -U user_name database_name`


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
