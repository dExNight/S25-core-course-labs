# Docker Role

Ansible role automates the installation and configuration of Docker and Docker Compose on Ubuntu systems

## Requirements

- Ansible 2.9+
- Ubuntu 22.04 or newer
- Python 3.x on target systems

## Role Variables

### Core Configuration
- `docker_edition`: Docker version to install (default: 'ce')
- `docker_compose_version`: Docker Compose version (default: 'v2.21.0')
- `docker_users`: List of users to add to docker group

### Docker Daemon Options
- `docker_daemon_options`: Configuration options for Docker daemon
  - `storage-driver`: Storage driver selection
  - `log-opts`: Logging configuration
  - `live-restore`: Container availability during daemon updates

## Example Usage

Basic implementation in a playbook:
```yaml
- hosts: servers
  roles:
    - role: docker
      vars:
        docker_users:
          - "{{ ansible_user_id }}"
        docker_daemon_options:
          storage-driver: "overlay2"
          log-opts:
            max-size: "100m"
            max-file: "3"
```

## Available Tags

The role provides several tags for selective execution:
- `docker`: Core Docker installation tasks
- `docker-compose`: Docker Compose installation
- `configuration`: Docker daemon configuration
- `service`: Service management tasks