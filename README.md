Ansible Role: Medusa-docker
===========================

Install Medusa Docker Compose project.

- https://pymedusa.com/
- https://github.com/pymedusa/Medusa

Based on LinuxServer.io image: https://docs.linuxserver.io/images/docker-medusa/

Requirements
------------

Requires the following to be installed:
- docker
- docker compose

Role Variables
--------------

Common system variables:

```yaml
timezone: UTC
```

Common Docker projects variables:

```yaml
# Base directory for Docker projects
docker_projects_path: # /var/apps
```

Available role variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker project variables

medusa_project_name: medusa

# Docker project dynamic vars (uses `docker_project_name` prefix, adapt if overridden)

medusa_traefik_loadbalancer_server_port: 8081


# Medusa project variables

# lscr.io/linuxserver/medusa image version
medusa_version: latest

# UID container is running as
medusa_puid: "{{ ansible_user_uid }}"
# GID container is running as
medusa_pgid: "{{ ansible_user_gid }}"

# Medusa network mode (bridge|host)
medusa_network_mode: bridge

medusa_media_volumes: []
#  # Downloads directory (blackhole)
#  - source: "/var/downloads"
#    target: "/downloads"
#
#  # Media directory
#  - source: "/share/media/series"
#    target: "/tv"
```

Dependencies
------------

This role depends on :
- [djuuu.docker_project](https://github.com/Djuuu/ansible-role-docker-project)

Some variables allow integration with:
- [djuuu.traefik_docker](https://github.com/Djuuu/ansible-role-traefik-docker)

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: true
  gather_subset:
    - "!all"
    - "!min"
    - user_id

  roles:
    - djuuu.medusa_docker
```

License
-------

Beerware License
