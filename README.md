# Тестовое задание

## Постановка задачи

Необходимо создать несколько ролей Ansible:

Роль номер 1: install-nginx:
В рамках данной роли необходимо установить nginx и добавить его в качестве демона systemd.
Для простоты считать что это один бинарный файл, который необходимо скачать из некоего registry по http и положить в /bin/
Для разных хостов registry может быть разным, но значение по умолчанию — https://example.com/registry/nginx_1.0.0
Юнит должен быть запущен из-под конкретного пользователя, которого можно задать в переменных группы\хоста, значение по умолчанию «nginx».
Если пользователя с таким именем не существует, он должен быть создан.
Помимо этого, для юнита должна быть задана переменная окружения NGINX_CONF_DIR, значение по умолчанию «/etc/nginx».
Если такой папки не существует, она должна быть создана, owner – пользователь, из-под которого запускается юнит, mode 700, group неважно.
Также в эту папку должны быть записаны темплейты конфиг-файлов по fileglob: “templates/nginx/*”  с правами 600 и owner тот же, что и у NGINX_CONF_DIR.

Роль номер 2: prepare-disk:
В рамках данной роли необходимо отформатировать диск по имени девайса (/dev/sda, /dev/sdb и так далее), которое для каждого хоста может быть разным, значение по умолчанию отсутствует.
В результате должна быть размечена одна партиция на весь диск с типом GPT.
Далее необходимо создать на данной партиции ФС (по своему выбору), после чего подмонтировать данную фс в папку /data.
Для простоты, содержимое /etc/fstab для каждого хоста заранее известно и выглядит так:
 /dev/disk/by-label/disk-ssd                       xfs     defaults        0 0

После чего необходимо создать плейбук с именем configure-webserver, который бы применял обе роли на хосты из группы ngx-webserver.

## Результат

Написаны две роли, находятся в директории roles.
Для простоты проверки можно развернуть инфраструктуру с помощью vagrant.
Vagrantfile находится в корне.
Некоторые таски не могут быть выполнены без ошибки, поэтому ошибки в них игнорируются и выполнение плейбука продолжается.
