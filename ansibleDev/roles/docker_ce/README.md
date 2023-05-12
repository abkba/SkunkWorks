# Install Docker

Role removes older packages of `docker` and installs specified version of
`docker-ce`.

## Prerequisites

- Rocky Linux 9
- uses `yum` to install packages
- All docker images should be manually removed prior to running this role. Some
  undesirable issues have been noticed managing images that weren't
  deleted/removed while the old packages removal process.

**To Run:** `ansible-playbook -i inventory playbooks/install-docker`

## Configure install
### Variables

- Role has default variables declared in `defaults/main.yml`, as so:

```yaml
---
# Old docker packages to remove
docker_old_packages:
  - docker
  - docker-client-latest
  - docker-client
  - docker-common
  - docker-latest
  - docker-latest-logrotate
  - docker-logrotate
  - docker-selinux
  - docker-engine-selinux
  - docker-engine

# Required yum packages
docker_yum_packages:
  - yum-utils
  - device-mapper-persistent-data
  - lvm2

# docker-ce repo url
docker_repo_url: "https://download.docker.com/linux/centos/docker-ce.repo"

# docker version
docker_ver: 17.09.0

# docker rpm to install
docker_rpm: "docker-ce-{{ docker_ver }}.ce"
```

As always, use the host_vars/group_vars to override these settings.

## Setup process

`main.yml`:
  - `remove_old_packages.yml`
  - `install_docker.yml`.

`remove_old_packages.yml`:
  - Creates file with packages to remove.
  - Notifies handler to remove packages if file changes.
  - Handler removes packages listed under `docker_old_packages`.

`install_docker.yml`:
  - Install required dependencies.
  - Copy docker-ce repo file and installs specified docker-ce version.

### TODO/Bugs

- Bug: Removes docker-ce, if `uninstall.docker` file is absent.
- TODO: Better installation process & messaging.
