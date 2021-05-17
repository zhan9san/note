# Tekton

## Core concepts

To build a CI/CD system with Tekton, you need to specify a Tekton pipeline. A pipeline consists of one or more Tekton tasks, each of which may include several steps. Additionally, a task may take some pipeline resources as inputs and outputs.

For example, if you plan to build a CI/CD system that builds source code from your GitHub repository into a container image, the Tekton pipeline may look as follows:

```text

GitHub repository(Pipeline Resource)

-->
Pipeline
1. Fetch source code from Github
2. Build source code into container image and push it to the registry

--->
Container Registry(Pipeline Resource)
```

## Setup

### Installing Tekton

```bash
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml
```

It may take a few moments for the installation to complete. To monitor the progress, run the following command:

```bash
kubectl get pods --namespace tekton-pipelines
```

Every component listed in the output should have the status `running`.

### Getting the code

We’ve put everything you need for this scenario in a GitHub repository. To clone this repository, run the following command:

```bash
git clone https://github.com/tektoncd/website
```

Open the directory `website/tutorials/katacoda/getting-started/src`. The directory consists of three subdirectories and one file:

* `app/`: a simple Python Flask web application.
* `tekton-katacoda/`: Tekton resource specifications you will use in this scenario.
* `Dockerfile`: a Dockerfile for building app/ into a runnable container image.

### Almost done

Tekton is now running in your Katacoda experimental cluster. To help the installation run smoothly in this special environment, a few extra steps are required:

```bash
mkdir /mnt/data && kubectl apply -f https://k8s.io/examples/pods/storage/pv-volume.yaml && \
kubectl apply -f ~/website/tutorials/katacoda/getting-started/src/tekton-katacoda/init.yaml && \
kubectl delete configmap/config-artifact-pvc -n tekton-pipelines && \
kubectl create configmap config-artifact-pvc --from-literal=storageClassName=manual -n tekton-pipelines
```

## Specifying Tekton tasks

As introduced earlier, a Tekton CI/CD workflow is a Tekton pipeline with a number of Tekton tasks, each of which performs an operation, such as retrieving source code or running the unit tests, in the workflow.

Tekton uses Kubernetes Custom Resource Definitions to specify Tekton resources (tasks, pipelines, etc.). To specify a task, for example, you need to create a YAML file as follows:
