### Обновление пакетов
```
sudo apt —reinstall install python3 -y

sudo apt —reinstall install python3-pip -y
```
На «Питоне» ботов для Telegram обычно пишут с помощью библиотеки TelegramBotAPI. Для ее установки введем команду:
```
pip3 install pyTelegramBotAPI
```
Теперь нам нужно установить удобный менеджер процессов PM2 и язык программирования NodeJS с менеджером пакетов npm для его работы:
```
sudo apt install nodejs

sudo apt install npm

npm install pm2 -g
```
Запуск бота
```
cd имя_папки
pm2 start main.py --interpreter=python3 --max-memory-restart 300M
```
Список запущенных скриптов
```
pm2 list
```