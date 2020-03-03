install-pkg-ubuntu
==================

[![Build Status](https://travis-ci.org/itnok/ansible-role-install-pkg-ubuntu.svg?branch=master)](https://travis-ci.org/itnok/ansible-role-install-pkg-ubuntu) [![GitHub tag](https://img.shields.io/github/v/tag/itnok/ansible-role-install-pkg-ubuntu?sort=semver)](https://github.com/itnok/ansible-role-install-pkg-ubuntu/tags/)

Makes it easier to add DEB repositories and install packages on an Ubuntu host.

Steps performed are:

  - Update apt package cache
  - Get list of available updates
  - Perform upgrade of all upgradable packages to the latest version
  - Check if reboot is required
  - Reboot of the machine if needed


:exclamation: Requirements
--------------------------

None.


:abcd: Role Variables
---------------------

None.


:link: Dependencies
-------------------

None.


:notebook: Example Playbook
---------------------------

Here an example of how to use this role in your playbooks:

```
---
- hosts: servers
  remote_user: ubuntu   # optional (your remote user)
  gather_facts: yes     # optional
  become: yes

  roles:
    - { role: itnok.install_pkg_ubuntu }

  vars:
    docker_dependency:    # Optional (Pick whatever name you like for this variable)
      - curl
      - software-properties-common
    install_pkg_dependency: "{{ install_pkg_dependency + docker_dependency }}"
    install_pkg_key:
      - "https://download.docker.com/linux/ubuntu/gpg"
    install_pkg_repo:
      - "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
      - "ppa:embrosyn/cinnamon"
      - "ppa:noobslab/macbuntu"
```

:guardsman: License
-------------------

MIT _([read more](LICENSE.md))_
