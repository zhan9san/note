# Kubernetes plugin

[How to get token and cert](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)

## Token

```bash
kubectl get secret $(kubectl get sa jenkins -o yaml | yq e '.secrets[0].name' -) -o yaml | yq e '.data.token' - | base64 -d
```

## Cert

```bash
kubectl get secret $(kubectl get sa jenkins -o yaml | yq e '.secrets[0].name' -) -o yaml | yq e '.data."ca.crt"' - | base64 -d
```
