# How to find which role or clusterrole binded to a service account in Kubernetes?

```bash
kubectl get rolebindings,clusterrolebindings \
  --all-namespaces  \
  -o custom-columns='KIND:kind,NAMESPACE:metadata.namespace,NAME:metadata.name,SERVICE_ACCOUNTS:subjects[?(@.kind=="ServiceAccount")].name' | grep "<SERVICE_ACCOUNT_NAME>"
```

Replace the grep with then name of the service account you are looking for.

---

Administrators can combine this with user impersonation to determine what action other users can perform.

```bash
kubectl auth can-i list secrets --namespace dev --as dave
```

kubectl auth can-i get deployments --as system:serviceaccount:default:default

kubectl get rolebindings,clusterrolebindings -o custom-columns='KIND:kind,NAMESPACE:metadata.namespace,NAME:metadata.name,SERVICE_ACCOUNTS:subjects[?(@.kind=="ServiceAccount")].name'

---

Katacode

```bash
$ kubectl get rolebindings,clusterrolebindings -o custom-columns='KIND:kind,NAMESPACE:metadata.namespace,NAME:metadata.name,SERVICE_ACCOUNTS:subjects[?(@.kind=="ServiceAccount")].name'
KIND                 NAMESPACE   NAME                                                   SERVICE_ACCOUNTS
ClusterRoleBinding   <none>      cluster-admin                                          <none>
ClusterRoleBinding   <none>      flannel                                                flannel
ClusterRoleBinding   <none>      kubeadm:get-nodes                                      <none>
ClusterRoleBinding   <none>      kubeadm:kubelet-bootstrap                              <none>
ClusterRoleBinding   <none>      kubeadm:node-autoapprove-bootstrap                     <none>
ClusterRoleBinding   <none>      kubeadm:node-autoapprove-certificate-rotation          <none>
ClusterRoleBinding   <none>      kubeadm:node-proxier                                   kube-proxy
ClusterRoleBinding   <none>      permissive-binding                                     <none>
ClusterRoleBinding   <none>      system:basic-user                                      <none>
ClusterRoleBinding   <none>      system:controller:attachdetach-controller              attachdetach-controller
ClusterRoleBinding   <none>      system:controller:certificate-controller               certificate-controller
ClusterRoleBinding   <none>      system:controller:clusterrole-aggregation-controller   clusterrole-aggregation-controller
ClusterRoleBinding   <none>      system:controller:cronjob-controller                   cronjob-controller
ClusterRoleBinding   <none>      system:controller:daemon-set-controller                daemon-set-controller
ClusterRoleBinding   <none>      system:controller:deployment-controller                deployment-controller
ClusterRoleBinding   <none>      system:controller:disruption-controller                disruption-controller
ClusterRoleBinding   <none>      system:controller:endpoint-controller                  endpoint-controller
ClusterRoleBinding   <none>      system:controller:endpointslice-controller             endpointslice-controller
ClusterRoleBinding   <none>      system:controller:expand-controller                    expand-controller
ClusterRoleBinding   <none>      system:controller:generic-garbage-collector            generic-garbage-collector
ClusterRoleBinding   <none>      system:controller:horizontal-pod-autoscaler            horizontal-pod-autoscaler
ClusterRoleBinding   <none>      system:controller:job-controller                       job-controller
ClusterRoleBinding   <none>      system:controller:namespace-controller                 namespace-controller
ClusterRoleBinding   <none>      system:controller:node-controller                      node-controller
ClusterRoleBinding   <none>      system:controller:persistent-volume-binder             persistent-volume-binder
ClusterRoleBinding   <none>      system:controller:pod-garbage-collector                pod-garbage-collector
ClusterRoleBinding   <none>      system:controller:pv-protection-controller             pv-protection-controller
ClusterRoleBinding   <none>      system:controller:pvc-protection-controller            pvc-protection-controller
ClusterRoleBinding   <none>      system:controller:replicaset-controller                replicaset-controller
ClusterRoleBinding   <none>      system:controller:replication-controller               replication-controller
ClusterRoleBinding   <none>      system:controller:resourcequota-controller             resourcequota-controller
ClusterRoleBinding   <none>      system:controller:route-controller                     route-controller
ClusterRoleBinding   <none>      system:controller:service-account-controller           service-account-controller
ClusterRoleBinding   <none>      system:controller:service-controller                   service-controller
ClusterRoleBinding   <none>      system:controller:statefulset-controller               statefulset-controller
ClusterRoleBinding   <none>      system:controller:ttl-controller                       ttl-controller
ClusterRoleBinding   <none>      system:coredns                                         coredns
ClusterRoleBinding   <none>      system:discovery                                       <none>
ClusterRoleBinding   <none>      system:kube-controller-manager                         <none>
ClusterRoleBinding   <none>      system:kube-dns                                        kube-dns
ClusterRoleBinding   <none>      system:kube-scheduler                                  <none>
ClusterRoleBinding   <none>      system:node                                            <none>
ClusterRoleBinding   <none>      system:node-proxier                                    <none>
ClusterRoleBinding   <none>      system:public-info-viewer                              <none>
ClusterRoleBinding   <none>      system:volume-scheduler                                <none>
ClusterRoleBinding   <none>      tekton-dashboard-backend                               tekton-dashboard
ClusterRoleBinding   <none>      tekton-dashboard-extensions                            tekton-dashboard
ClusterRoleBinding   <none>      tekton-dashboard-tenant                                tekton-dashboard
ClusterRoleBinding   <none>      tekton-pipelines-controller-cluster-access             tekton-pipelines-controller
ClusterRoleBinding   <none>      tekton-pipelines-controller-tenant-access              tekton-pipelines-controller
ClusterRoleBinding   <none>      tekton-pipelines-webhook-cluster-access                tekton-pipelines-webhook
```

```bash
$ kubectl get clusterrolebinding/permissive-binding -o yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  creationTimestamp: "2021-05-19T16:14:07Z"
  managedFields:
  - apiVersion: rbac.authorization.k8s.io/v1
    fieldsType: FieldsV1
    fieldsV1:
      f:roleRef:
        f:apiGroup: {}
        f:kind: {}
        f:name: {}
      f:subjects: {}
    manager: kubectl
    operation: Update
    time: "2021-05-19T16:14:07Z"
  name: permissive-binding
  resourceVersion: "272"
  selfLink: /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/permissive-binding
  uid: 1baf904b-1487-46d9-a14f-44705ee5310d
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: admin
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: kubelet
- apiGroup: rbac.authorization.k8s.io
  kind: Group
  name: system:serviceaccounts
```
