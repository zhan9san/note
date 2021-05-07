# NodePort in Minikube

`https://github.com/kubernetes/minikube/issues/11193`

```bash
minikube start --driver=docker --extra-config=apiserver.service-node-port-range=32760-32767 --ports=127.0.0.1:32760-32767:32760-32767

```
