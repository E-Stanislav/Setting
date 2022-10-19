### Create the file repository configuration.
```
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```
### Import the repository signing key.
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```
### Update the package lists.
```
sudo apt-get update
```
### Install PostgreSQL 13 on Debian 10.x versions using below command.
```
sudo apt-get -y install postgresql-13
```
### Check the PostgreSQL server on Debian status by using following command.
```
systemctl status postgresql
```
### Lets connect to PostgreSQL server using.
```
sudo su - postgres
psql
```
### Change the postgres user password on Debian Linux
```
alter user postgres with password 'admin@123';
```
### Create new user with pass and add privilegies
```
CREATE USER master WITH LOGIN PASSWORD 'admin@123' SUPERUSER CREATEDB CREATEROLE INHERIT;	
```
### Open TCP/IP for connect
##### File: postgresql.conf
```
listen_addresses = '*'	
```
##### File: pg_hba.conf
##### Add line
```
host    all         all         {your_ip_address}/24        md5
```