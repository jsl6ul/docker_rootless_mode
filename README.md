# Ansible Collection - jsl6ul.docker_rootless_mode

Ansible collection to run the Docker daemon and containers as a non-root user.

You must define `docker_rootless_user`, see the example in `common/defaults/main.yml`.

You can use this collection using ansible-galaxy.

```
$ cat requirements.yml
---
collections:
  - name: git@github.com:jsl6ul/docker_rootless_mode.git
    type: git
    version: main

$ ansible-galaxy install -r requirements.yml
```
