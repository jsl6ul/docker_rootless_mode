# ansible role to configure a rootless mode docker host

based on https://docs.docker.com/engine/security/rootless/

Tested with Debian 11, Debian 12.

This role makes changes to limits and capabilities/cgroups, you should reboot the host after the initial setup.


# Debian 12

There's a problem with debian 12, the compilation of `pyyaml` (for python's docker-compose module) 
depends on `cython`, and the latest version of cython 3 seems incompatible with debian 12. For the time 
being, the solution is to limit to `cython < 3`, with a `pip_constraint` file.

In addition, debian 12 does not want to install system-wide pip modules without warning. 
You must therefore add `break-system-packages = true` to `pip.conf`.

The role takes care of these situations, see the role files for details.


# playbook example

```
- name: Setup rootless docker host
  hosts: some_docker_host
  become: true
  roles:
    - role: jsl6ul.docker_rootless_mode.host
```
