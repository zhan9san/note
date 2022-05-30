
<https://github.com/kubernetes/minikube/issues/13768>

minikube offline start failed

Digest is lost after loading a saved image
<https://github.com/moby/moby/issues/22011>


<https://github.com/kubernetes/minikube/issues/10075>
Fix handling of image digests in the minikube cache

Calculate digest from tarball #895
<https://github.com/google/go-containerregistry/issues/895>


Docker build should compute image digests #32016
<https://github.com/moby/moby/issues/32016>

Fix handling of image digests in the minikube cache #10075
<https://github.com/kubernetes/minikube/issues/10075>

---
Report sha256 digest in docker inspect #17670
<https://github.com/moby/moby/issues/17670>


---
cn mirror

Host preload image on a site accessible from China: Get Alibaba account for minikube #7695
<https://github.com/kubernetes/minikube/issues/7695>

request: recurring to fund Alibaba account for minikube #14
<https://github.com/kubernetes/funding/issues/14>

China Firewall: Adding Aliyun mirror for preload images and K8s release binaries #12578
<https://github.com/kubernetes/minikube/pull/12578>


---
Intresting issue

Works only when I specify --base-image #11068
<https://github.com/kubernetes/minikube/issues/11068>


```
rm -rf .minikube/cache/*

minikube start --download-only=true --driver=docker --alsologtostderr -v=8 --base-image=google_containers/kicbase:v0.0.30

unset http_proxy https_proxy all_proxy

scp -r ~/.minikube/cache vagrant@192.168.31.49:~/.minikube/
scp -r ~/.minikube/cache vagrant@10.66.40.21:~/.minikube/

minikube start --download-only=true --driver=docker --alsologtostderr -v=8 --image-mirror-country=cn --base-image=registry.cn-hangzhou.aliyuncs.com/google_containers/kicbase:v0.0.30

minikube start --driver=docker --alsologtostderr -v=8 --image-mirror-country=cn

minikube start --driver=docker --alsologtostderr -v=8 --image-mirror-country=cn --base-image=registry.cn-hangzhou.aliyuncs.com/google_containers/kicbase:v0.0.30

minikube start --driver=docker --alsologtostderr -v=8 --base-image=google_containers/kicbase:v0.0.30

minikube start --driver=docker --alsologtostderr -v=8 --base-image=gcr.io/k8s-minikube/kicbase:v0.0.30 --image-mirror-country=cn --download-only=true

minikube start --driver=docker --alsologtostderr -v=8 --base-image=gcr.io/k8s-minikube/kicbase:v0.0.30

minikube start --driver=docker --alsologtostderr -v=8 --base-image=gcr.io/k8s-minikube/kicbase:v0.0.30 --download-only=true

minikube start --driver=docker --image-mirror-country=cn --base-image=registry.cn-hangzhou.aliyuncs.com/google_containers/kicbase:v0.0.30

minikube start --driver=docker --image-mirror-country=cn --base-image=registry.cn-hangzhou.aliyuncs.com/google_containers/kicbase:v0.0.30 --docker-opt=restart=unless-stopped

docker tag
```
