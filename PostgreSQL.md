#PostgreSQL 9 cheat sheet

##Backup and restore a database

###First method using a zipped file
####Backup
pg_dump -Fc -U postgres -f file_name.dump database_name
####Restore
psql -U postgres -c "DROP DATABASE IF EXISTS database_name;"
psql -U postgres -c "CREATE DATABASE database_name OWNER role_name ENCODING 'UTF-8';"
psql -U postgres -d database_name -c "DROP EXTENSION IF EXISTS plpgsql;"
pg_restore -d database_name -j 4 -U postgres -O --role=role_name file_name.dump

###Second method using a SQL script
####Backup
pg_dump -U postgres --create --clean -f file_name.sql database_name
####Restore
psql -U postgres -d database_name -f file_name.sql

##Administration

To be continued
