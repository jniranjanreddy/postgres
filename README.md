# postgres
## https://www.mockaroo.com/
# Source - https://www.youtube.com/watch?v=qw--VYLpxG4&list=PLxtrcgLvnR2Yjj4mIbL1aspC_XzVNvP_6
## DB Mate is used for DB migrations.. 
```
docker volume create postgres_data

docker run --name postgres_container \
    -e POSTGRES_PASSWORD=mysecretpassword \
    -d -p 5432:5432 \
    -v postgres_data:/var/lib/postgresql/data \
    postgres


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
```
root@minikube01 ~ # helm install postgresql bitnami/postgresql-ha
NAME: postgresql
LAST DEPLOYED: Thu Apr 20 10:31:30 2023
NAMESPACE: cafe
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: postgresql-ha
CHART VERSION: 11.3.0
APP VERSION: 15.2.0
** Please be patient while the chart is being deployed **
PostgreSQL can be accessed through Pgpool via port 5432 on the following DNS name from within your cluster:

    postgresql-postgresql-ha-pgpool.cafe.svc.cluster.local

Pgpool acts as a load balancer for PostgreSQL and forward read/write connections to the primary node while read-only connections are forwarded to standby nodes.

To get the password for "postgres" run:

    export POSTGRES_PASSWORD=$(kubectl get secret --namespace cafe postgresql-postgresql-ha-postgresql -o jsonpath="{.data.password}" | base64 -d)

To get the password for "repmgr" run:

    export REPMGR_PASSWORD=$(kubectl get secret --namespace cafe postgresql-postgresql-ha-postgresql -o jsonpath="{.data.repmgr-password}" | base64 -d)

To connect to your database run the following command:

    kubectl run postgresql-postgresql-ha-client --rm --tty -i --restart='Never' --namespace cafe --image docker.io/bitnami/postgresql-repmgr:15.2.0-debian-11-r16 --env="PGPASSWORD=$POSTGRES_PASSWORD"  \
        --command -- psql -h postgresql-postgresql-ha-pgpool -p 5432 -U postgres -d postgres

To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace cafe svc/postgresql-postgresql-ha-pgpool 5432:5432 &
    psql -h 127.0.0.1 -p 5432 -U postgres -d postgres
root@minikube01 ~ #

```
## how to create user and DB.
```
CREATE USER "user1" WITH PASSWORD 'user_password';
CREATE DATABASE my-db WITH OWNER "user1";


CREATE DATABASE yourdbname;
CREATE USER youruser WITH ENCRYPTED PASSWORD 'yourpass';
GRANT ALL PRIVILEGES ON DATABASE yourdbname TO youruser;
```
