# ServiceAccount

Minikube

```bash
kubectl get po myapp-run-1621391324676-build-hnf78-pod-lm56m -o yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"tekton.dev/v1alpha1","kind":"Task","metadata":{"annotations":{},"name":"build-docker","namespace":"default"},"spec":{"inputs":{"params":[{"default":"./Dockerfile","description":"Path to the Dockerfile to build.","name":"DOCKERFILE"},{"default":"./","description":"The build context used by Docker.","name":"CONTEXT"},{"default":"myapp:latest","description":"The image on which builds will run","name":"BUILDER_IMAGE"}],"resources":[{"name":"source","type":"git"}]},"steps":[{"args":["build","-f","$(inputs.params.DOCKERFILE)","-t","$(inputs.params.BUILDER_IMAGE)","$(inputs.params.CONTEXT)"],"command":["docker"],"image":"docker","name":"docker","volumeMounts":[{"mountPath":"/var/run/docker.sock","name":"docker-socket"},{"mountPath":"/var/lib/docker","name":"docker-library"}],"workingDir":"/workspace/source"}],"volumes":[{"hostPath":{"path":"/var/run/docker.sock","type":"Socket"},"name":"docker-socket"},{"hostPath":{"path":"/var/lib/docker"},"name":"docker-library"}]}}
    pipeline.tekton.dev/release: v0.20.0
    tekton.dev/ready: READY
  creationTimestamp: "2021-05-19T02:28:44Z"
  labels:
    app: tekton-app
    app.kubernetes.io/managed-by: tekton-pipelines
    tekton.dev/pipeline: myapp
    tekton.dev/pipelineRun: myapp-run-1621391324676
    tekton.dev/pipelineTask: build
    tekton.dev/task: build-docker
    tekton.dev/taskRun: myapp-run-1621391324676-build-hnf78
  name: myapp-run-1621391324676-build-hnf78-pod-lm56m
  namespace: default
  ownerReferences:
  - apiVersion: tekton.dev/v1beta1
    blockOwnerDeletion: true
    controller: true
    kind: TaskRun
    name: myapp-run-1621391324676-build-hnf78
    uid: bc8dac4b-80d6-46c5-a1e7-6245e6ae82d9
  resourceVersion: "2917"
  selfLink: /api/v1/namespaces/default/pods/myapp-run-1621391324676-build-hnf78-pod-lm56m
  uid: 9d29ca93-0c98-4100-a708-7c4a37cd15cb
spec:
  containers:
  - args:
    - -wait_file
    - /tekton/downward/ready
    - -wait_file_content
    - -post_file
    - /tekton/tools/0
    - -termination_path
    - /tekton/termination
    - -entrypoint
    - /ko-app/git-init
    - --
    - -url
    - https://github.com/zhan9san/myapp
    - -path
    - /workspace/source
    - -revision
    - master
    command:
    - /tekton/tools/entrypoint
    env:
    - name: HOME
      value: /tekton/home
    - name: TEKTON_RESOURCE_NAME
      value: source
    - name: HOME
      value: /tekton/home
    image: gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/git-init:v0.20.0@sha256:6b6a8fd4a7aeae8995a4acd2b2fb77458c287b309f2ccabdb257a067f37521b8
    imagePullPolicy: IfNotPresent
    name: step-git-source-source-sdltw
    resources:
      requests:
        cpu: "0"
        ephemeral-storage: "0"
        memory: "0"
    terminationMessagePath: /tekton/termination
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /tekton/tools
      name: tekton-internal-tools
    - mountPath: /tekton/downward
      name: tekton-internal-downward
    - mountPath: /tekton/creds
      name: tekton-creds-init-home-llz5p
    - mountPath: /workspace
      name: tekton-internal-workspace
    - mountPath: /tekton/home
      name: tekton-internal-home
    - mountPath: /tekton/results
      name: tekton-internal-results
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-hwr8v
      readOnly: true
    workingDir: /workspace
  - args:
    - -wait_file
    - /tekton/tools/0
    - -post_file
    - /tekton/tools/1
    - -termination_path
    - /tekton/termination
    - -entrypoint
    - docker
    - --
    - build
    - -f
    - ./Dockerfile
    - -t
    - myapp:latest
    - ./
    command:
    - /tekton/tools/entrypoint
    env:
    - name: HOME
      value: /tekton/home
    image: docker
    imagePullPolicy: Always
    name: step-docker
    resources:
      requests:
        cpu: "0"
        ephemeral-storage: "0"
        memory: "0"
    terminationMessagePath: /tekton/termination
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/docker.sock
      name: docker-socket
    - mountPath: /var/lib/docker
      name: docker-library
    - mountPath: /tekton/tools
      name: tekton-internal-tools
    - mountPath: /tekton/creds
      name: tekton-creds-init-home-fx9nz
    - mountPath: /workspace
      name: tekton-internal-workspace
    - mountPath: /tekton/home
      name: tekton-internal-home
    - mountPath: /tekton/results
      name: tekton-internal-results
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-hwr8v
      readOnly: true
    workingDir: /workspace/source
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  initContainers:
  - args:
    - -c
    - mkdir -p /workspace/source
    command:
    - sh
    image: gcr.io/distroless/base@sha256:92720b2305d7315b5426aec19f8651e9e04222991f877cae71f40b3141d2f07e
    imagePullPolicy: IfNotPresent
    name: working-dir-initializer
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /workspace
      name: tekton-internal-workspace
    - mountPath: /tekton/home
      name: tekton-internal-home
    - mountPath: /tekton/results
      name: tekton-internal-results
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-hwr8v
      readOnly: true
    workingDir: /workspace
  - command:
    - /ko-app/entrypoint
    - cp
    - /ko-app/entrypoint
    - /tekton/tools/entrypoint
    image: gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/entrypoint:v0.20.0@sha256:9621a893ae2d4eb91fa8d56bf6f15774be8abd26e5d3f5e10a3f8eb8f31d540a
    imagePullPolicy: IfNotPresent
    name: place-tools
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /tekton/tools
      name: tekton-internal-tools
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-hwr8v
      readOnly: true
  nodeName: minikube
  priority: 0
  restartPolicy: Never
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - emptyDir: {}
    name: tekton-internal-workspace
  - emptyDir: {}
    name: tekton-internal-home
  - emptyDir: {}
    name: tekton-internal-results
  - emptyDir: {}
    name: tekton-internal-tools
  - downwardAPI:
      defaultMode: 420
      items:
      - fieldRef:
          apiVersion: v1
          fieldPath: metadata.annotations['tekton.dev/ready']
        path: ready
    name: tekton-internal-downward
  - emptyDir:
      medium: Memory
    name: tekton-creds-init-home-llz5p
  - emptyDir:
      medium: Memory
    name: tekton-creds-init-home-fx9nz
  - hostPath:
      path: /var/run/docker.sock
      type: Socket
    name: docker-socket
  - hostPath:
      path: /var/lib/docker
      type: ""
    name: docker-library
  - name: default-token-hwr8v
    secret:
      defaultMode: 420
      secretName: default-token-hwr8v
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2021-05-19T02:29:04Z"
    reason: PodCompleted
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2021-05-19T02:29:48Z"
    reason: PodCompleted
    status: "False"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2021-05-19T02:29:48Z"
    reason: PodCompleted
    status: "False"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2021-05-19T02:28:44Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: docker://27067192c61a97037d0d4be78dcc20708228a3e8b96dbc15db15d9643f0e1b20
    image: docker:latest
    imageID: docker-pullable://docker@sha256:ad50b8d78b41dc52f42ab123ce0e3f48c54437ed70ecc2a44c99e889924c8e56
    lastState: {}
    name: step-docker
    ready: false
    restartCount: 0
    started: false
    state:
      terminated:
        containerID: docker://27067192c61a97037d0d4be78dcc20708228a3e8b96dbc15db15d9643f0e1b20
        exitCode: 0
        finishedAt: "2021-05-19T02:30:36Z"
        message: '[{"key":"StartedAt","value":"2021-05-19T02:29:46.936Z","type":"InternalTektonResult"}]'
        reason: Completed
        startedAt: "2021-05-19T02:29:40Z"
  - containerID: docker://b35b0d2d87b9cdf808cb39aafacc1751964853a50a04947e384d1250ab810192
    image: sha256:b462f3c6ba0a564fdf28f41d8464092805b3133120e23f6588c13c313cbe285b
    imageID: docker-pullable://gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/git-init@sha256:6b6a8fd4a7aeae8995a4acd2b2fb77458c287b309f2ccabdb257a067f37521b8
    lastState: {}
    name: step-git-source-source-sdltw
    ready: false
    restartCount: 0
    started: false
    state:
      terminated:
        containerID: docker://b35b0d2d87b9cdf808cb39aafacc1751964853a50a04947e384d1250ab810192
        exitCode: 0
        finishedAt: "2021-05-19T02:29:46Z"
        message: '[{"key":"commit","value":"ee47db81928ac9cc1c72d3706beb18a8d4650ca5","resourceName":"source","resourceRef":{"name":"source"}},{"key":"url","value":"https://github.com/zhan9san/myapp","resourceName":"source","resourceRef":{"name":"source"}},{"key":"StartedAt","value":"2021-05-19T02:29:43.846Z","type":"InternalTektonResult"}]'
        reason: Completed
        startedAt: "2021-05-19T02:29:05Z"
  hostIP: 192.168.49.2
  initContainerStatuses:
  - containerID: docker://1ae84c325b8d3c899f938faf05612ce25dafcc95e9f058ed219c2a1180ed0214
    image: gcr.io/distroless/base@sha256:92720b2305d7315b5426aec19f8651e9e04222991f877cae71f40b3141d2f07e
    imageID: docker-pullable://gcr.io/distroless/base@sha256:92720b2305d7315b5426aec19f8651e9e04222991f877cae71f40b3141d2f07e
    lastState: {}
    name: working-dir-initializer
    ready: true
    restartCount: 0
    state:
      terminated:
        containerID: docker://1ae84c325b8d3c899f938faf05612ce25dafcc95e9f058ed219c2a1180ed0214
        exitCode: 0
        finishedAt: "2021-05-19T02:28:58Z"
        reason: Completed
        startedAt: "2021-05-19T02:28:58Z"
  - containerID: docker://2b53fded8e833ee3a2b62d063d02377db801ca54519a8ce8929c4b17de7d3c2b
    image: sha256:a01696cd60bdd7e350af10bed82cddb21f8f358765fc4f1041380475b26da2a2
    imageID: docker-pullable://gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/entrypoint@sha256:9621a893ae2d4eb91fa8d56bf6f15774be8abd26e5d3f5e10a3f8eb8f31d540a
    lastState: {}
    name: place-tools
    ready: true
    restartCount: 0
    state:
      terminated:
        containerID: docker://2b53fded8e833ee3a2b62d063d02377db801ca54519a8ce8929c4b17de7d3c2b
        exitCode: 0
        finishedAt: "2021-05-19T02:29:02Z"
        reason: Completed
        startedAt: "2021-05-19T02:29:02Z"
  phase: Succeeded
  podIP: 172.17.0.6
  podIPs:
  - ip: 172.17.0.6
  qosClass: BestEffort
  startTime: "2021-05-19T02:28:45Z"
```

```bash
kubectl get po myapp-run-1621412487418-deploy-mtb2b-pod-2lgt8 -o yaml
```

```yaml

apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"tekton.dev/v1alpha1","kind":"Task","metadata":{"annotations":{},"name":"deploy-kubectl","namespace":"default"},"spec":{"inputs":{"params":[{"default":"config/","description":"Path to the directory for kubectl apply -f","name":"K8S_DIRECTORY_PATH"}],"resources":[{"name":"source","type":"git"}]},"steps":[{"args":["apply","-f","$(inputs.params.K8S_DIRECTORY_PATH)"],"command":["kubectl"],"image":"lachlanevenson/k8s-kubectl","name":"apply-config","workingDir":"/workspace/source"}]}}
    pipeline.tekton.dev/release: v0.20.0
    tekton.dev/ready: READY
  creationTimestamp: "2021-05-19T08:22:05Z"
  labels:
    app: tekton-app
    app.kubernetes.io/managed-by: tekton-pipelines
    tekton.dev/pipeline: myapp
    tekton.dev/pipelineRun: myapp-run-1621412487418
    tekton.dev/pipelineTask: deploy
    tekton.dev/task: deploy-kubectl
    tekton.dev/taskRun: myapp-run-1621412487418-deploy-mtb2b
  name: myapp-run-1621412487418-deploy-mtb2b-pod-2lgt8
  namespace: default
  ownerReferences:
  - apiVersion: tekton.dev/v1beta1
    blockOwnerDeletion: true
    controller: true
    kind: TaskRun
    name: myapp-run-1621412487418-deploy-mtb2b
    uid: 90b0cd13-07ba-4477-b85c-2a8c64141e46
  resourceVersion: "9258"
  selfLink: /api/v1/namespaces/default/pods/myapp-run-1621412487418-deploy-mtb2b-pod-2lgt8
  uid: c91ad59b-73c6-4aba-9187-90bd92e377b0
spec:
  containers:
  - args:
    - -wait_file
    - /tekton/downward/ready
    - -wait_file_content
    - -post_file
    - /tekton/tools/0
    - -termination_path
    - /tekton/termination
    - -entrypoint
    - /ko-app/git-init
    - --
    - -url
    - https://github.com/zhan9san/myapp
    - -path
    - /workspace/source
    - -revision
    - master
    command:
    - /tekton/tools/entrypoint
    env:
    - name: HOME
      value: /tekton/home
    - name: TEKTON_RESOURCE_NAME
      value: source
    - name: HOME
      value: /tekton/home
    image: gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/git-init:v0.20.0@sha256:6b6a8fd4a7aeae8995a4acd2b2fb77458c287b309f2ccabdb257a067f37521b8
    imagePullPolicy: IfNotPresent
    name: step-git-source-source-vkg62
    resources:
      requests:
        cpu: "0"
        ephemeral-storage: "0"
        memory: "0"
    terminationMessagePath: /tekton/termination
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /tekton/tools
      name: tekton-internal-tools
    - mountPath: /tekton/downward
      name: tekton-internal-downward
    - mountPath: /tekton/creds
      name: tekton-creds-init-home-fz2pr
    - mountPath: /workspace
      name: tekton-internal-workspace
    - mountPath: /tekton/home
      name: tekton-internal-home
    - mountPath: /tekton/results
      name: tekton-internal-results
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-l7l9g
      readOnly: true
    workingDir: /workspace
  - args:
    - -wait_file
    - /tekton/tools/0
    - -post_file
    - /tekton/tools/1
    - -termination_path
    - /tekton/termination
    - -entrypoint
    - kubectl
    - --
    - apply
    - -f
    - config/
    command:
    - /tekton/tools/entrypoint
    env:
    - name: HOME
      value: /tekton/home
    image: lachlanevenson/k8s-kubectl
    imagePullPolicy: Always
    name: step-apply-config
    resources:
      requests:
        cpu: "0"
        ephemeral-storage: "0"
        memory: "0"
    terminationMessagePath: /tekton/termination
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /tekton/tools
      name: tekton-internal-tools
    - mountPath: /tekton/creds
      name: tekton-creds-init-home-kg6zs
    - mountPath: /workspace
      name: tekton-internal-workspace
    - mountPath: /tekton/home
      name: tekton-internal-home
    - mountPath: /tekton/results
      name: tekton-internal-results
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-l7l9g
      readOnly: true
    workingDir: /workspace/source
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  initContainers:
  - args:
    - -c
    - mkdir -p /workspace/source
    command:
    - sh
    image: gcr.io/distroless/base@sha256:92720b2305d7315b5426aec19f8651e9e04222991f877cae71f40b3141d2f07e
    imagePullPolicy: IfNotPresent
    name: working-dir-initializer
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /workspace
      name: tekton-internal-workspace
    - mountPath: /tekton/home
      name: tekton-internal-home
    - mountPath: /tekton/results
      name: tekton-internal-results
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-l7l9g
      readOnly: true
    workingDir: /workspace
  - command:
    - /ko-app/entrypoint
    - cp
    - /ko-app/entrypoint
    - /tekton/tools/entrypoint
    image: gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/entrypoint:v0.20.0@sha256:9621a893ae2d4eb91fa8d56bf6f15774be8abd26e5d3f5e10a3f8eb8f31d540a
    imagePullPolicy: IfNotPresent
    name: place-tools
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /tekton/tools
      name: tekton-internal-tools
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-l7l9g
      readOnly: true
  nodeName: node01
  priority: 0
  restartPolicy: Never
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - emptyDir: {}
    name: tekton-internal-workspace
  - emptyDir: {}
    name: tekton-internal-home
  - emptyDir: {}
    name: tekton-internal-results
  - emptyDir: {}
    name: tekton-internal-tools
  - downwardAPI:
      defaultMode: 420
      items:
      - fieldRef:
          apiVersion: v1
          fieldPath: metadata.annotations['tekton.dev/ready']
        path: ready
    name: tekton-internal-downward
  - emptyDir:
      medium: Memory
    name: tekton-creds-init-home-fz2pr
  - emptyDir:
      medium: Memory
    name: tekton-creds-init-home-kg6zs
  - name: default-token-l7l9g
    secret:
      defaultMode: 420
      secretName: default-token-l7l9g
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2021-05-19T08:22:07Z"
    reason: PodCompleted
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2021-05-19T08:22:11Z"
    reason: PodCompleted
    status: "False"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2021-05-19T08:22:11Z"
    reason: PodCompleted
    status: "False"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2021-05-19T08:22:05Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: docker://fa63e9648a1a5ba19dcdaca09ef839af03c38c61391d89a4f3b9665f27243f6b
    image: lachlanevenson/k8s-kubectl:latest
    imageID: docker-pullable://lachlanevenson/k8s-kubectl@sha256:5a2840cfc2f59162e96efce635e7b5baa56b6f50d721467152ab042e2ab64803
    lastState: {}
    name: step-apply-config
    ready: false
    restartCount: 0
    started: false
    state:
      terminated:
        containerID: docker://fa63e9648a1a5ba19dcdaca09ef839af03c38c61391d89a4f3b9665f27243f6b
        exitCode: 0
        finishedAt: "2021-05-19T08:22:13Z"
        message: '[{"key":"StartedAt","value":"2021-05-19T08:22:11.592Z","type":"InternalTektonResult"}]'
        reason: Completed
        startedAt: "2021-05-19T08:22:08Z"
  - containerID: docker://bd2e679d60bbb17db8d0098cfb220fd642e12a76848fa4309e71a90b5ee30580
    image: sha256:b462f3c6ba0a564fdf28f41d8464092805b3133120e23f6588c13c313cbe285b
    imageID: docker-pullable://gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/git-init@sha256:6b6a8fd4a7aeae8995a4acd2b2fb77458c287b309f2ccabdb257a067f37521b8
    lastState: {}
    name: step-git-source-source-vkg62
    ready: false
    restartCount: 0
    started: false
    state:
      terminated:
        containerID: docker://bd2e679d60bbb17db8d0098cfb220fd642e12a76848fa4309e71a90b5ee30580
        exitCode: 0
        finishedAt: "2021-05-19T08:22:11Z"
        message: '[{"key":"commit","value":"ee47db81928ac9cc1c72d3706beb18a8d4650ca5","resourceName":"source","resourceRef":{"name":"source"}},{"key":"url","value":"https://github.com/zhan9san/myapp","resourceName":"source","resourceRef":{"name":"source"}},{"key":"StartedAt","value":"2021-05-19T08:22:10.725Z","type":"InternalTektonResult"}]'
        reason: Completed
        startedAt: "2021-05-19T08:22:07Z"
  hostIP: 172.17.0.37
  initContainerStatuses:
  - containerID: docker://cfdd71eda645c1ea8c210d0149ddebcb3c755311187fec6e517af75b9cf9023a
    image: sha256:4dc0ba3700ab0dcc162f67da9481a906f7753f171c08f602db6667fd74151f07
    imageID: docker-pullable://gcr.io/distroless/base@sha256:92720b2305d7315b5426aec19f8651e9e04222991f877cae71f40b3141d2f07e
    lastState: {}
    name: working-dir-initializer
    ready: true
    restartCount: 0
    state:
      terminated:
        containerID: docker://cfdd71eda645c1ea8c210d0149ddebcb3c755311187fec6e517af75b9cf9023a
        exitCode: 0
        finishedAt: "2021-05-19T08:22:05Z"
        reason: Completed
        startedAt: "2021-05-19T08:22:05Z"
  - containerID: docker://d19f6ea66b2378d46f51e7f409490c2d3712ed161d52927cc6bf61d1137fd141
    image: sha256:a01696cd60bdd7e350af10bed82cddb21f8f358765fc4f1041380475b26da2a2
    imageID: docker-pullable://gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/entrypoint@sha256:9621a893ae2d4eb91fa8d56bf6f15774be8abd26e5d3f5e10a3f8eb8f31d540a
    lastState: {}
    name: place-tools
    ready: true
    restartCount: 0
    state:
      terminated:
        containerID: docker://d19f6ea66b2378d46f51e7f409490c2d3712ed161d52927cc6bf61d1137fd141
        exitCode: 0
        finishedAt: "2021-05-19T08:22:06Z"
        reason: Completed
        startedAt: "2021-05-19T08:22:06Z"
  phase: Succeeded
  podIP: 10.244.1.8
  podIPs:
  - ip: 10.244.1.8
  qosClass: BestEffort
  startTime: "2021-05-19T08:22:04Z"
```
