### Update Your System.
```
sudo apt update
```
### Get the Docker Compose repository.
```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
### Modify File Permissions.
```
sudo chmod +x /usr/local/bin/docker-compose
```
### Check Docker Version.
```
docker-compose --version
```