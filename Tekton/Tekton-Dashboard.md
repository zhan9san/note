# Tekton Dashboard

Introduction to the Tekton Dashboard
In this tutorial, we will go through:

* Installing the Tekton Dashboard
* Importing a Tekton Pipeline using the Tekton Dashboard
* Creating a PipelineResource using the Tekton Dashboard
* Creating a PipelineRun using the Tekton Dashboard
* Monitoring the logs of a PipelineRun using the Tekton Dashboard

## Install the Tekton Dashboard Prerequisites

```bash
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/previous/v0.20.0/release.yaml
```

Verify the pods are running:

```bash
kubectl get pods -n tekton-pipelines
```

## Install the Tekton Dashboard

For reference, the installation instructions are [here](https://github.com/tektoncd/dashboard#install-dashboard). To install the Tekton Dashboard, run the following command:

```bash
kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/previous/v0.13.0/tekton-dashboard-release.yaml
```

Verify the Dashboard pod is running:

```bash
kubectl get pods -n tekton-pipelines
```

## Expose the Tekton Dashboard

View the Tekton Dashboard Service:

```bash
kubectl get svc tekton-dashboard -n tekton-pipelines
```

The Tekton Dashboard Service is exposed on port `9097`. So, set up a port forward for the `tekton-dashboard` Service on port `9097`:

```bash
kubectl port-forward -n tekton-pipelines --address=0.0.0.0 service/tekton-dashboard 80:9097 > /dev/null 2>&1 &
```

## Open the Tekton Dashboard

Open the Dashboard tab in your Katacoda window, or click on the following link: https://2886795297-80-kitek05.environments.katacoda.com/.

It might take a minute for the ingress and Katacoda to get set up.

### Import Tekton Resources for MyApp

In this section, we will import a Tekton Pipeline to build and deploy the demo Nodejs app called [MyApp](https://github.com/ncskier/myapp). MyApp displays a random picture of a cat.

#### Open the Tekton Dashboard Import Tekton resources page

Click on the following link to go directly to the Import Tekton resources page: https://2886795297-80-kitek05.environments.katacoda.com/#/importresources

Or navigate to the Import Tekton resources page in the Dashboard.

#### Import the MyApp Tekton resources

We want to import the Tekton resources that are defined in the [tekton/](https://github.com/ncskier/myapp/tree/master/tekton) directory of MyApp. Import these Tekton resources into the default Namespace by filling in the form with the following information:

Repository URL: `https://github.com/ncskier/myapp`

Repository path: `tekton/`

Target namespace: `default`

Expand the 'Advanced configuration' section and fill in the following:

Service Account: `tekton-dashboard`

Leave the default values for the rest of the fields.

The form should look like the following:
cat << EOF | kubectl apply -f -
apiVersion: tekton.dev/v1alpha1
kind: PipelineRun
metadata:
  name: myapp
spec:
  pipelineRef:
    name: myapp
  resources:
    - name: source
      resourceSpec:
        type: git
        params:
          - name: revision
            value: main
          - name: url
            value: https://github.com/ncskier/myapp
EOF