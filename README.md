# Дефолтная настройка сервера
Здесь я пишу скрипт для лёгкой настройки после установки Ubuntu server'a

## Логинишься
Теперь заходим под супер-пользователем. Это удобно чтоб не писать перед каждой командой sudo
```sudo -s```

Вводишь пароль

### Поехали пакеты
Обновляем пакеты сначала первой командой, потом второй. Это занимает время, просто ждем
```apt update```
```apt upgrade```

Теперь устанавливаем на сервер адекватную дату для отображения всего что будет на сервере
```timedatectl set-timezone Europe/Moscow``` это утснавливает время МСК, если что, можешь найди другие таймзоны и изменить Europe/Mosxow

sudo apt-get install openssh-server

sudo apt-get install ufw

sudo ufw enable

sudo ufw allow 22
sudo ufw allow 8080
sudo ufw allow 5657
sudo ufw allow 80
sudo ufw allow 433

УСТАНОВКА СТЕКА ЛАМП (это база)

sudo apt install apache2

sudo systemctl start apache2

sudo apt install mysql-server

sudo systemctl start mysql

sudo apt install php libapache2-mod-php php-mysql

sudo apt install php

Тут каждому своё, это не обязательно УСТАНОВКА PUFFERPANEL (для меня удобная панелька для майнкрафт хоста + сайт)

curl -s https://packagecloud.io/install/repositories/pufferpanel/pufferpanel/script.deb.sh | sudo bash

sudo apt-get install pufferpanel=2.7.0

sudo pufferpanel user add

*Вводишь имя, почту и пароль, в целом на похуй можно просто admin, admin@admin.ru и тд (у меня лично так) в конце главное там где ADMIN (Y/N) ставь Y типо админ аккаунт*

sudo systemctl enable --now pufferpanel

Дальше переходишь на http://ТВОЙ_АЙПИ:8080 и всё работает)


ДЕЛАЕМ SFTP ДОСТУП ЧЕРЕЗ FILEZILLA С ПОЛНЫМИ ПРАВАМИ (удобно файлики загружать)

sudo passwd root
Задаем пароль

sudo apt-get install ssh

sudo nano /etc/ssh/sshd_config

В конфиге находишь строчку PermitRootLogin, если перед ней "#" удалчешь "#" и строчка должна выглядеть так PermitRootLogin yes

Закрываешь файл: Ctrl+S, Ctrl+X

sudo service ssh restart

Для подключения в filezilla

Хост:твой_айпи
Пользователь: root
Пароль: который_установили_для_root

И всё, полный доступ ко всем файлам всей машины(не безопасно, но удобно). Чтоб отключить - просто в конфиге PermitRootLogin no
