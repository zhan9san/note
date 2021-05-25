# Install kubectl

`https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-binary-with-curl-on-linux`

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

If the owner of kubectl is root, there will be an error

```bash
$ kubectl get po
error: no server found for cluster "minikube"
```

But no error when it is invoked by absolute path.

```bash
$ /usr/local/bin/kubectl get po
No resources found in default namespace.
```

If `kubectl` was copied to another location, it works well

```bash
$ cp /usr/local/bin/kubectl /tmp/
$ cd /tmp
$ ./kubectl get po
No resources found in default namespace.
```

Latest update

If we run kubectl in relative mode, it doesn't wokr.
Instead, absolute mode works.

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-0.32.0/deploy/static/provider/kind/deploy.yaml

kubectl wait -n ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
