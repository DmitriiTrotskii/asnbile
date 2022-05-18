Docker-host
=========

Описание
--------------

- Установка дополнительных пакетов (полный список: ```apt_tools_install```)
  - apt over https, ntp
- Установка python3, и  настройка alternatives в случае присуствия python2
- Установка полседней версии docker (полный список: ```apt_docker_install```)
- Запуск portainer, в случае необходимости
- Pull docker images, в случае необходимости

Переменные
--------------

```default_admin_user -> str```

Пользователь, который будет назначен администратором. Этому пользователю, так же, будут добавлены ключи ssh. 

---

```ssh_pub_keys -> list``` 

Список публичных ключей, которые будут добавленны пользователю.

---

```python2_alt_value -> str && python3_alt_value -> str```

Значения для приоритета альтернативных исполняемых файлов python.

---

```apt_https_install -> list```

Список пектов для работы APT через HTTPs.

---

```apt_tools_install -> list```

Список дополнительных пакетов.

---

```apt_docker_install -> list```

Сисок пакетов Docker.

---

```docker_url -> str```

Ссылка на репозиторий Docker.

---

```ntp_server -> str```

Адрес NTP сервера.

---

```portainer -> bool```

Указывает, на необходимость установки docker portainer container.

---

```images -> str``` ```[pull | undefinded]```

Указывает, на необходимость скачать образы docker.

---

```images_pull -> list```

Список образов, которые будут скачанны.

---

Зависимости
------------

Необходим модуль community.docker

Для установки:

```shell
ansible-galaxy collection install community.docker
```

Пример Playbook
----------------
```yaml
  - name: Prepare docker server
    hosts: "{{ HOSTS }}"
    gather_facts: true
    become: yes

    roles:
      - docker-host
```
Запуск playbook:
```shell
ansible-playbook docker-host.yaml -e "HOSTS=docker"
```
Дополнительно запустить portainer:
```shell
ansible-playbook docker-host.yaml -e "HOSTS=docker" -e "portainer=yes"
```
Дополнительно сказать образы:
```shell
ansible-playbook docker-host.yaml -e "HOSTS=docker" -e "images=pull"
```