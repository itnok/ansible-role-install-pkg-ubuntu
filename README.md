manage-pkg-ubuntu
==================

[![Build Status](https://travis-ci.org/itnok/ansible-role-install-pkg-ubuntu.svg?branch=master)](https://travis-ci.org/itnok/ansible-role-install-pkg-ubuntu) [![GitHub tag](https://img.shields.io/github/v/tag/itnok/ansible-role-install-pkg-ubuntu?sort=semver)](https://github.com/itnok/ansible-role-install-pkg-ubuntu/tags/) [![Ansible Role](https://img.shields.io/ansible/role/47006)](https://galaxy.ansible.com/itnok/manage_pkg_ubuntu)

Makes it easier to add DEB repositories and install packages on an Ubuntu host.

Steps performed are:

  - Update apt package cache
  - Make sure all needed dependency packages are installed
  - Add all keys used to authenticate deb trusted packages
  - Add all apt repositories
  - Refresh apt package cache for new repos
  - Add all deb packages


## :exclamation: Requirements
-----------------------------

None.


## :abcd: Role Variables
------------------------

| Variable                   | Description                                                               | Default Value                                         |
|----------------------------|---------------------------------------------------------------------------|-------------------------------------------------------|
| `__manage_pkg_dependency` | Default dependencies needed by the role                                   | `[apt-transport-https, ca-certificates, gnupg-agent]` |
| `manage_pkg_key`          | List of keys to add ([Check Example](#notebook-example-playbook))                  | `[]`                                                  |
| `manage_pkg_repo`         | List of deb repositories ([Check Example](#notebook-example-playbook) for formats) | `[]`                                                  |
| `manage_pkg_dependency`   | List of dependencies                                                      | `"{{ __manage_pkg_dependency }}"`                    |
| `manage_pkg_app`          | List of applications to install                                           | `[]`                                                  |


## :link: Dependencies
----------------------

None.


## :notebook: Example Playbook
------------------------------

Here an example of how to use this role in your playbooks:

```
---
- hosts: servers
  remote_user: ubuntu   # optional (your remote user)
  gather_facts: yes     # optional
  become: yes

  roles:
    - { role: itnok.manage_pkg_ubuntu }

  vars:
    docker_dependency:    # optional (Pick whatever name you like for this variable)
      - curl
      - software-properties-common
    manage_pkg_dependency: "{{ manage_pkg_dependency + docker_dependency }}"
    manage_pkg_key:
      - "https://download.docker.com/linux/ubuntu/gpg"
    manage_pkg_repo:
      - "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
      - "ppa:embrosyn/cinnamon"
      - "ppa:noobslab/macbuntu"
    manage_pkg_app:
      - "cinnamon"
      - "docker-ce"
      - "macbuntu-os-icons-v1804"
      - "macbuntu-os-ithemes-v1804"
      - "macbuntu-os-plank-theme-v1804"
      - "plank"
```

## :guardsman: License
----------------------

MIT _([read more](LICENSE.md))_
