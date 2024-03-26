# ansible role to configure a rootless mode docker host

based on https://docs.docker.com/engine/security/rootless/

Tested with Debian 11, Debian 12.

This role makes changes to limits and capabilities/cgroups, you should reboot the host after the initial setup.


# playbook example

```
- name: Setup rootless docker host
  hosts: some_docker_host
  become: true
  roles:
    - role: jsl6ul.docker_rootless_mode.host
```
