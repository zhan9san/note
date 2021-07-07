# Container Runtime

## Kubernetes Container Runtimes

1. Docker Engine
2. CRI-O
3. CRI Containerd
4. gVisor
5. CRI-O Kata Containers.

Essentially a container runtime is responsible for pulling down images from a registry, expanding them on disk and then executing them in a namespace.

The first three are traditional container runtimes that start containers in their own namespace. The latter two are new runtimes that provide extra isolation. Here’s a quick overview of the differences.

Docker Engine, CRI-O and CRI containerd all use the same underlying technology(runC) to start contaienrs.

---

How a container gets created in a Kubernetes environment. At a high level, conceptually here is what is happening:

```bash
Orchestration API -> Container Engine API -> Kernel API
```

Digging one level deeper, here’s what it actually looks like today in most production setups:

```bash
Kubernetes Master -> Kubelet -> Docker Engine -> containerd -> runc -> Linux kernel
```

In OpenShift Online we are moving to this architecture, also in the OpenShift Container Platform product:

```bash

```

## Reference

[Kubernetes Container Runtimes](https://kubedex.com/kubernetes-container-runtimes/)
