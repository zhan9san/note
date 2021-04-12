# Cert

Use Host-IP mapping for another cluster

```shell script
kubectl --kubeconfig=config-demo get po -A
Unable to connect to the server: x509: certificate is valid for minikubeCA, control-plane.minikube.internal, kubernetes.default.svc.cluster.local, kubernetes.default.svc, kubernetes.default, kubernetes, localhost, not a.com
```

Use IP for another cluster

```shell script
Unable to connect to the server: x509: certificate is valid for 192.168.49.2, 10.96.0.1, 127.0.0.1, 10.0.0.1, not 172.28.24.96
```
