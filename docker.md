### Обновление пакетов
```
apt update
```
### Установите пакеты, которые необходимы для работы пакетного менеджера apt по протоколу HTTPS:
```
apt install apt-transport-https ca-certificates curl software-properties-common
```
### Добавьте GPG-ключ репозитория Docker:
```
curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
### Добавьте репозиторий Docker:
```
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list  /dev/null
```
### Обновление пакетов
```
apt update
```
### Переключитесь в репозиторий Docker, чтобы его установить:
```
apt-cache policy docker-ce
```
### Установите Docker:
```
apt install docker-ce
```
### Проверьте работоспособность программы:
```
systemctl status docker
```