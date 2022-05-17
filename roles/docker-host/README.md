Docker-host
=========

Переменные
--------------

- ```default_admin_user -> str```: Пользователь, который будет назначен администратором docker и которому, будут добавлены ключи ssh. 
  - default: ```default_admin_user = root```

ssh_pub_keys -> list: Список публичных ключей, которые будут добавленны пользователю.
default: 
  ssh_pub_keys = ["{{ lookup('file', lookup('env','HOME') + '/.ssh/id_rsa.pub') }}"]

python2_alt_value -> str && python3_alt_value -> str: Значения для приоритета альтернативных исполняемых файлов python.
default:
  python2_alt_value = "10"
  python3_alt_value = "20"

apt_https_install -> list: Установка пектов для работы APT через HTTPs.
default:
  apt_https_install = [ca-certificates, curl, gnupg, lsb-release, apt-transport-https]

apt_tools_install -> list: Установка дополнительных пакетов.
default:
  apt_tools_install = [tree, net-tools, mc, htop, git]

apt_docker_install -> list: Устанвока пакетов Docker.
default:
  apt_docker_install = [docker-ce, docker-ce-cli, containerd.io, docker-compose]

docker_url -> str: Ссылка на репозиторий Docker.
default:
  docker_url = "https://download.docker.com/linux/ubuntu"

ntp_server -> str: Адрес NTP сервера.
default:
  ntp_server = "{{ ansible_default_ipv4.gateway }}"

portainer -> bool: Указывает, на необходимость установки docker portainer container.
default:
  portainer = undefined

images -> str: Указывает, на необходимость скачать образы docker.
default:
  iamges = undefined

images_pull -> list: Список образов, которые будут скачанны.
default:
  images_pull = [ubuntu:latest, alpine:latest, postgres:latest, mysql:latest, nginx:latest]

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
