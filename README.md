# Ansible Collection - jsl6ul.docker_rootless_mode

Ansible collection to run the Docker daemon and containers as a non-root user.
You must define `docker_rootless_user`, see the example in `common/defaults/main.yml`.

You can install this collection with ansible-galaxy.

```
$ cat requirements.yml
---
collections:
  - name: https://github.com/jsl6ul/docker_rootless_mode.git
    type: git
    version: main

$ ansible-galaxy install -r requirements.yml
```

## Using this collection

Deploy the `host` role using root, and `user` role as the `docker_rootless_user.name`.

```
- name: rootless docker host
  hosts: ahost
  become: true
  tasks:
    - name: Import role jsl6ul.docker_rootless_mode.host
      ansible.builtin.import_role:
        name: jsl6ul.docker_rootless_mode.host

- name: Setup rootless docker user and containers
  hosts: ahost
  user: "{{ docker_rootless_user.name }}"
  become: false
  tasks:
    - name: Import role jsl6ul.docker_rootless_mode.user
      ansible.builtin.import_role:
        name: jsl6ul.docker_rootless_mode.user

    - name: Import role jsl6ul.docker_apps.traefik
      ansible.builtin.import_role:
        name: jsl6ul.docker_apps.traefik

    - name: Import role jsl6ul.docker_apps.glances
      ansible.builtin.import_role:
        name: jsl6ul.docker_apps.glances
```
