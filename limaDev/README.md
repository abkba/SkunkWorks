# Lima Development

Projects around getting various linux machines/workflows running on Mac using
Lima.

## Dependencies

Have `lima` pre-installed on your Mac computer

```
brew install lima
```

## Setup

This is still work in progress.

### docker-machine

Currently we just have a Rocky Linux 9 compatible vm config, that can run as
your docker-machine (with containerd backend). The main idea was to have a
more light-weight alternative to Docker Desktop or Rancher Desktop, something
along the lines of Colima, but more readable and open.

#### Usage

1. Run `limactl start docker-machines/RockyLinux9/config.yaml` and wait for the
   vm instance to build.

2. Point your `DOCKER_HOST` environment variable to `tcp://127.0.0.1:62376` or
   create a context config using
   `docker context create <name> --docker "host=tcp://127.0.0.1:62376`.

3. gg

## TODO

- More supported config files for docker-machine
- Better automation around usage
- minikube/k8s setup support
