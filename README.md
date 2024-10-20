# WireGuard VPS Playbook

Плейбук для настройки wg-easy с помощью Ansible.

## Требовавния

Для использования плейбука необходимы:

- python v3.12.6
- ansible v2.16.11
- pipenv

Плейбук рассчитан на настройку хостов с Debian 12.

## Использование

Подготовьте VPS для подключения по SSH.

Создайте инвентарь ваших серверов в `inventories/production` по аналогии с `inventories/dev/hosts`.

Установите зависимости

```sh
ansible-galaxy install -r requirements.yml
```
Запустите настройку

```sh
ansible-playbook -i inventories/production playbook.yml -K
```

По завершении выполнения плейбука на VPS будет развернут [wg-easy](https://github.com/wg-easy/wg-easy) с помощью `docker`. Доступ к веб-интерфейсу из внешней сети заблокирован. Чтобы подключиться к веб-интерфейсу используйте команду

```sh
ssh -L 3000:127.0.0.1:51821 <your-user>@<your-vps-address>
```

Пока активна сессия SSH вы сможете подключиться к веб-интерфейсу wg-easy по адресу `localhost:3000`. 