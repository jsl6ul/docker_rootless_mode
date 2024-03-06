# ansible role to configure the user account running the docker container in rootless mode

Containers are configured with an unprivileged user. Interactions are made with `systemd --user`.

This role must be called using this user, and `become:false`. 
`su`, `sudo` or ansible `become` won't work because it bypasses some pam configurations, and prevents `systemd --user` from working properly.

The umask of this unprivileged user must be `0002` to avoid write permission problems with bind mount volumes.

# playbook example

```
- name: Setup rootless docker user
  hosts: some_docker_host
  user: "{{ docker_rootless_user.name }}"
  become: false
  roles:
    - role: jsl6ul.docker_rootless_mode.user
```
