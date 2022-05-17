Docker-host
=========

Переменные
--------------

```default_admin_user -> str``` Пользователь, который будет назначен администратором docker и которому, будут добавлены ключи ssh. 

```ssh_pub_keys -> list``` Список публичных ключей, которые будут добавленны пользователю.

```python2_alt_value -> str && python3_alt_value -> str``` Значения для приоритета альтернативных исполняемых файлов python.

```apt_https_install -> list``` Список пектов для работы APT через HTTPs.

```apt_tools_install -> list``` Список дополнительных пакетов.

```apt_docker_install -> list``` Сисок пакетов Docker.

```docker_url -> str``` Ссылка на репозиторий Docker.

```ntp_server -> str``` Адрес NTP сервера.

```portainer -> bool``` Указывает, на необходимость установки docker portainer container.

```images -> str``` ```[pull | undefinded]``` Указывает, на необходимость скачать образы docker.

```images_pull -> list``` Список образов, которые будут скачанны.

Зависимости
------------

Для развертывания portainer в процессе установки необхоим модуль community.docker.
Будет установлен автоматически на хосте с которого запускается ansible.

Пример Playbook
----------------
```yaml
  - name: Prepare docker server
    hosts: "{{ HOSTS }}"
    gather_facts: true
    become: yes

    roles:
      - dkr
```
