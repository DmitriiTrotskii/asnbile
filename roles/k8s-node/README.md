k8s-node
=========

Подготавливает хост для добавления в кластер k8s через kubeadm.


Переменные
--------------

mirantis_url -> str:
default: 
  mirantis_url = "https://raw.githubusercontent.com/Mirantis/cri-dockerd/master/packaging/systemd/"

cri_ver -> str:
default:
  cri_ver = "v0.2.0"

k8s_gpg_url -> str:
default:
  k8s_gpg_url = "https://packages.cloud.google.com/apt/doc/apt-key.gpg"

k8s_deb_url -> str:
default:
  k8s_deb_url: "https://apt.kubernetes.io/ kubernetes-xenial main"

apt_k8s_install -> list:
default:
  apt_k8s_install: [kubelet, kubeadm, kubectl]

Зависимости
------------

- role/docker-host

Пример Playbook
----------------

  - name: Prepare k8s node
    hosts: "{{ HOSTS }}"
    gather_facts: true
    become: yes

    roles:
      - docker-host
      - k8s-node