# Настройка ноутбука для работы как сервера (без выключения при закрытии крышки)

## Краткое описание
Инструкция по настройке Ubuntu 22.04 LTS для предотвращения выключения ноутбука при закрытии крышки. Это позволит использовать ноутбук как постоянный сервер.

---

## Способ 1: Настройка через systemd (Рекомендуемый)

### Шаг 1: Откройте файл конфигурации logind

```bash
sudo nano /etc/systemd/logind.conf
```

### Шаг 2: Найдите и измените параметры

В файле найдите секцию `[Login]` и измените следующие параметры:

```
[Login]
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```

**Значения параметров:**
- `HandleLidSwitch=ignore` — игнорировать закрытие крышки (ноутбук продолжает работать)
- `HandleLidSwitchExternalPower=ignore` — игнорировать закрытие крышки при подключении к сети
- `HandleLidSwitchDocked=ignore` — игнорировать закрытие крышки в режиме док-станции

Если строки закомментированы (начинаются с `#`), раскомментируйте их, удалив `#`.

### Шаг 3: Сохраните файл и перезапустите сервис

В редакторе nano нажмите:
- `Ctrl+O` — для сохранения
- `Enter` — для подтверждения
- `Ctrl+X` — для выхода

Затем перезапустите сервис:

```bash
sudo systemctl restart systemd-logind
```

### Шаг 4: Проверка

Закройте крышку ноутбука и убедитесь, что:
- Ноутбук продолжает работать (индикаторы питания не гаснут)
- По SSH можно подключиться к ноутбуку

---

## Способ 2: Использование команды без редактирования файла

Альтернативный способ — применить настройки командой:

```bash
sudo sed -i 's/#HandleLidSwitch=.*/HandleLidSwitch=ignore/' /etc/systemd/logind.conf
sudo sed -i 's/#HandleLidSwitchExternalPower=.*/HandleLidSwitchExternalPower=ignore/' /etc/systemd/logind.conf
sudo sed -i 's/#HandleLidSwitchDocked=.*/HandleLidSwitchDocked=ignore/' /etc/systemd/logind.conf
sudo systemctl restart systemd-logind
```

---

## Способ 3: Дополнительная настройка — запрет пробуждения при открытии крышки

Чтобы ноутбук НЕ пробуждался автоматически при открытии крышки (опционально):

### Шаг 1: Создайте файл конфигурации

```bash
sudo nano /etc/systemd/sleep.conf
```

### Шаг 2: Добавьте параметры

В секцию `[Sleep]` добавьте:

```
[Sleep]
HandleLidSwitch=ignore
AllowSuspend=no
AllowHibernate=no
```

### Шаг 3: Сохраните и перезапустите

```bash
sudo systemctl restart systemd-logind
```

---

## Проверка текущих настроек

Посмотреть текущие значения параметров:

```bash
sudo grep -E "HandleLidSwitch" /etc/systemd/logind.conf
```

---

## Возможные проблемы и решения

### Проблема 1: Настройки не применяются

**Решение:** Проверьте, что сервис запущен:

```bash
sudo systemctl status systemd-logind
```

### Проблема 2: Ноутбук все равно выключается

**Решение:** Проверьте, что нет других управляющих программ (например, TLP):

```bash
sudo tlp-stat --cfg
```

Если TLP установлен и настроен, измените в `/etc/tlp.conf`:

```
USB_AUTOSUSPEND=0
USB_BLACKLIST=*
```

### Проблема 3: Ноутбук сильно нагревается при закрытой крышке

**Решение:** Уменьшите энергопотребление:

```bash
# Установите утилиты управления питанием
sudo apt update && sudo apt install tlp thermald

# Включите службы
sudo systemctl enable tlp
sudo systemctl start tlp
sudo systemctl enable thermald
sudo systemctl start thermald
```

---

## Дополнительные рекомендации для сервера

### 1. Отключите сон по таймеру
```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

### 2. Настройте статический IP (если нужно)
Файл `/etc/netplan/00-installer-config.yaml`:

```yaml
network:
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
  version: 2
```

Применить настройки:
```bash
sudo netplan apply
```

### 3. Включите автозапуск нужных служб
```bash
sudo systemctl enable nginx  # пример для веб-сервера
sudo systemctl start nginx
```

---

## Отмена настроек (возврат к стандартному поведению)

Чтобы ноутбук снова засыпал при закрытии крышки:

```bash
sudo nano /etc/systemd/logind.conf
```

Измените значения на:

```
HandleLidSwitch=suspend
```

Или закомментируйте строки:

```
#HandleLidSwitch=suspend
```

Перезапустите сервис:

```bash
sudo systemctl restart systemd-logind
```

---

## Полезные команды

| Команда | Описание |
|---------|----------|
| `sudo systemctl status systemd-logind` | Статус службы logind |
| `journalctl -u systemd-logind -f` | Просмотр логов в реальном времени |
| `systemctl suspend` | Ручной перевод в спящий режим |
| `systemctl poweroff` | Выключение |
| `systemctl reboot` | Перезагрузка |

---

## Примечание

Настроив ноутбук для работы как сервера, помните:
- Ноутбук должен стоять на твердой поверхности для нормального охлаждения
- При закрытой крышке вентиляция может быть менее эффективной
- Рекомендуется периодически проверять температуру: `sensors` (установите пакет `lm-sensors`)
