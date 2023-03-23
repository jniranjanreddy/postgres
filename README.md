# postgres

```
docker run --name postgres -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword -d postgres
psql -h 192.168.9.87 -U airflow-user -d airflow_db

## How to install only postgres clien (psql)
apt-get install -y postgresql-client

docker exec -it postgres bash

root@9379397fe62c:/# su postgres

postgres@9379397fe62c:/$ psql
psql (14.2 (Debian 14.2-1.pgdg110+1))
Type "help" for help.

postgres=# \conninfo
You are connected to database "postgres" as user "postgres" via socket in "/var/run/postgresql" at port "5432".
postgres=#

postgres=# \q
```
## How to take backup
pg_dump --host=127.0.0.1 -U <Postgre_user> -W -F t Postgre_DB > Backup-filename.tar


## How to restore postges database.
pg_restore -U <Postgre_user> -W --host=127.0.0.1 --dbname=<Postgre_DB> --verbose Backup-filename.tar

## How to alter password
ALTER USER USERNAME WITH PASSWORD 'PASSWORD';
