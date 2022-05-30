# Debug

```bash
vagrant@vagrant:~$ minikube start --driver=docker --alsologtostderr -v=8 --image-mirror-country=cn --base-image=registry.cn-hangzhou.aliyuncs.com/google_containers/kicbase:v0.0.30 --cache-images=false
```

```bash
vagrant@vagrant:~$ minikube ssh
docker@minikube:~$ docker images
REPOSITORY                                                                    TAG       IMAGE ID       CREATED         SIZE
registry.cn-hangzhou.aliyuncs.com/google_containers/kube-apiserver            v1.23.3   f40be0088a83   6 weeks ago     135MB
registry.cn-hangzhou.aliyuncs.com/google_containers/kube-controller-manager   v1.23.3   b07520cd7ab7   6 weeks ago     125MB
registry.cn-hangzhou.aliyuncs.com/google_containers/kube-proxy                v1.23.3   9b7cc9982109   6 weeks ago     112MB
registry.cn-hangzhou.aliyuncs.com/google_containers/kube-scheduler            v1.23.3   99a3486be4f2   6 weeks ago     53.5MB
registry.cn-hangzhou.aliyuncs.com/google_containers/etcd                      3.5.1-0   25f8c7f3da61   4 months ago    293MB
registry.cn-hangzhou.aliyuncs.com/google_containers/coredns                   v1.8.6    a4ca41631cc7   5 months ago    46.8MB
registry.cn-hangzhou.aliyuncs.com/google_containers/pause                     3.6       6270bb605e12   6 months ago    683kB
registry.cn-hangzhou.aliyuncs.com/google_containers/storage-provisioner       v5        6e38f40d628d   11 months ago   31.5MB
```

pkg/minikube/image/cache.go

change image name in this file

pkg/minikube/bootstrapper/images/images.go

"k8s.io/minikube/pkg/minikube/constants"

cache

```text
vagrant@vagrant:~$ tree .minikube/cache/
.minikube/cache/
├── images
│   └── amd64
│       └── registry.cn-hangzhou.aliyuncs.com
│           └── google_containers
│               ├── coredns
│               │   └── coredns_v1.8.6
│               ├── etcd_3.5.1-0
│               ├── k8s-minikube
│               │   └── storage-provisioner_v5
│               ├── kube-apiserver_v1.23.3
│               ├── kube-controller-manager_v1.23.3
│               ├── kube-proxy_v1.23.3
│               ├── kubernetesui
│               │   ├── dashboard_v2.3.1
│               │   └── metrics-scraper_v1.0.7
│               ├── kube-scheduler_v1.23.3
│               └── pause_3.6
└── linux
    └── amd64
        └── v1.23.3
            ├── kubeadm
            ├── kubectl
            └── kubelet

10 directories, 13 files
```

```text
  "registry.cn-hangzhou.aliyuncs.com/google_containers/kube-apiserver:v1.23.3",
  "registry.cn-hangzhou.aliyuncs.com/google_containers/kube-controller-manager:v1.23.3",
  "registry.cn-hangzhou.aliyuncs.com/google_containers/kube-proxy:v1.23.3",
  "registry.cn-hangzhou.aliyuncs.com/google_containers/kube-scheduler:v1.23.3",
  "registry.cn-hangzhou.aliyuncs.com/google_containers/etcd:v1.23.3",
  "registry.cn-hangzhou.aliyuncs.com/google_containers/coredns:v1.23.3",
  "registry.cn-hangzhou.aliyuncs.com/google_containers/pause:v1.23.3",
```

`minikube start`

```bash
$ minikube start --download-only=true --driver=docker --image-mirror-country=cn
😄  minikube v1.25.2 on Ubuntu 21.04 (vbox/amd64)
✨  Using the docker driver based on user configuration

🧯  The requested memory allocation of 1978MiB does not leave room for system overhead (total system memory: 1978MiB). You may face stability issues.
💡  Suggestion: Start minikube with less memory allocated: 'minikube start --memory=1978mb'

✅  Using image repository registry.cn-hangzhou.aliyuncs.com/google_containers
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
    > kubectl.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
    > kubeadm.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
    > kubelet.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
    > kubectl: 44.43 MiB / 44.43 MiB [-------------] 100.00% 994.33 KiB p/s 46s
    > kubeadm: 43.12 MiB / 43.12 MiB [-------------] 100.00% 888.29 KiB p/s 50s
    > kubelet: 118.75 MiB / 118.75 MiB [------------] 100.00% 1.73 MiB p/s 1m9s
    > registry.cn-hangzhou.aliyun...: 379.06 MiB / 379.06 MiB  100.00% 3.26 MiB
✅  Download complete!

$ vagrant@vagrant:~$ tree .minikube/cache/
.minikube/cache/
├── images
│   └── amd64
│       └── registry.cn-hangzhou.aliyuncs.com
│           └── google_containers
│               ├── coredns_v1.8.6
│               ├── dashboard_v2.3.1
│               ├── etcd_3.5.1-0
│               ├── kube-apiserver_v1.23.3
│               ├── kube-controller-manager_v1.23.3
│               ├── kube-proxy_v1.23.3
│               ├── kube-scheduler_v1.23.3
│               ├── metrics-scraper_v1.0.7
│               ├── pause_3.6
│               └── storage-provisioner_v5
├── kic
│   └── amd64
│       └── kicbase_v0.0.30@sha256_02c921df998f95e849058af14de7045efc3954d90320967418a0d1f182bbc0b2.tar
└── linux
    └── amd64
        └── v1.23.3
            ├── kubeadm
            ├── kubectl
            └── kubelet

9 directories, 14 files
```

```shell
minikube start --driver=docker --image-mirror-country=cn --alsologtostderr -v=8
```
