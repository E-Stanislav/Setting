### Обновление пакетов
```
sudo apt update
apt update
```
### Установите пакеты, которые необходимы для работы пакетного менеджера apt по протоколу HTTPS:
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
apt install apt-transport-https ca-certificates curl software-properties-common
```
### Добавьте GPG-ключ репозитория Docker:
```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
### Добавьте репозиторий Docker:
```
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list  /dev/null
```
### Обновление пакетов
```
sudo apt update
apt update
```
### Переключитесь в репозиторий Docker, чтобы его установить:
```
apt-cache policy docker-ce
```
### Установите Docker:
```
sudo apt install docker-ce
apt install docker-ce
```
### Проверьте работоспособность программы:
```
sudo systemctl status docker
systemctl status docker
```