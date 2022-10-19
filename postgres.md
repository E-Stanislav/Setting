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
alter user postgres with password 'aasasa@14232';
```