# Minikube

[minikube hyperkit](https://minikube.sigs.k8s.io/docs/drivers/hyperkit/)
[docker desktop alternatives](https://devopstales.github.io/home/docker-desktop-alternatives/)

Ansible test depends on `systemd`, but there is some known issues
[Unable to run systemd services on Docker Desktop 4.3.0](https://github.com/docker/for-mac/issues/6073) and
[Running systemctl in container fails with "Failed to get D-Bus connection"](https://github.com/moby/moby/issues/2296)
in Docker for Mac. `Minikube` works well with `molecule`.

```bash
# Install minikube
$ brew install minikube
# Make hyperkit the default driver:
$ minikube config set driver hyperkit
# Start local cluster
$ minikube start
# Consume docker env
$ eval $(minikube docker-env)
```

## Molecule Systemd Container

[systemd-container](https://molecule.readthedocs.io/en/latest/examples.html#systemd-container)

There is no need to add `tmpfs`.

```yaml
platforms:
  - name: instance
    image: centos:8
    command: /sbin/init
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:ro
```
