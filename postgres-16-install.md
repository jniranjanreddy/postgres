## How to install postgres-16 in Ubuntu 22
```
sudo apt update
sudo apt install gnupg2 wget nano

sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg

sudo apt update

sudo apt install postgresql-16 postgresql-contrib-16

sudo systemctl start postgresql
sudo systemctl enable postgresql


vi /etc/postgresql/16/main/postgresql.conf
listen_addresses = '*'

sudo sed -i '/^host/s/ident/md5/' /etc/postgresql/16/main/pg_hba.conf
sudo sed -i '/^local/s/peer/trust/' /etc/postgresql/16/main/pg_hba.conf
echo "host all all 0.0.0.0/0 md5" | sudo tee -a /etc/postgresql/16/main/pg_hba.conf



ufw allow 5432/tcp
sudo -u postgres psql

ALTER USER postgres PASSWORD 'VeryStronGPassWord@1137';

CREATE DATABASE airflowdb;
CREATE USER airflowuser WITH ENCRYPTED PASSWORD 'VeryStronGPassWord@1137';
GRANT ALL PRIVILEGES ON DATABASE airflowdb TO airflowuser;

```
