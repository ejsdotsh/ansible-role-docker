Ansible Role: Docker
====================

an ansible role to install docker on debian/ubuntu

Requirements
------------

none

Role Variables
--------------

available variables are listed below, along with default values (see defaults/main.yml):

docker service options

```sh
docker_service: started
docker_service_enabled: true
```

debian/ubuntu options

```sh
# 'stable' or 'test'
docker_apt_release: test
# 'amd64' or 'arm64'
docker_apt_arch: amd64
docker_apt_repo: "deb [arch={{ docker_apt_arch }}] https://download.docker.com/linux/{{ ansible_distribution|lower }} {{ ansible_distribution_release }} {{ docker_apt_release }}"
docker_apt_ignore_key_error: true
docker_apt_gpg_key: https://download.docker.com/linux/{{ ansible_distribution|lower }}/gpg
```

a list of users to be added to the `docker` group (so they don't have to use `sudo` to run docker commands)

```sh
docker_users: []
```

Dependencies
------------

none

Example Playbook
----------------

this role is heavily modeled on [geerlingguy.docker](https://github.com/geerlingguy/ansible-role-docker), and modified to add variables to support zfs and multiple hardware architectures

```yaml
---
- name: install docker
  hosts: all
  tasks:
    include_role:
      name: joshuaejs.docker
    vars:
      # override default storage driver
      docker_storage_driver: zfs
      # 'amd64' or 'arm64' - defaults to amd64
      docker_apt_arch: amd64
```

License
-------

MIT

Author Information
------------------

this role was created in 2020 by [joshuaejs](https://github.com/joshuaejs)
