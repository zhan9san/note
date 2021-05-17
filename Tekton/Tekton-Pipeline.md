# Tekton Pipeline

## Create a basic Task

In this section, we will build the first task.

With Tekton, each operation in your CI/CD workflow becomes a Step, which is executed with a container image you specify. Steps are then organized in Tasks, which run as a Kubernetes pod in your cluster. You can further organize Tasks into Pipelines, which can control the order of execution of several Tasks.

To create a Task, create a Kubernetes object using the Tekton API with the kind Task. The following YAML file specifies a Task with one simple Step, which prints a Hello World! message using the official Ubuntu image:

task-hello.yaml

```yml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: hello
spec:
  steps:
    - name: hello
      image: ubuntu
      command:
        - echo
      script: |
        set -e
        echo "Hello World!"
```

Write the YAML above to a file named task-hello.yaml, and apply it to your Kubernetes cluster:

```bash
kubectl apply -f task-hello.yaml
```

To run this task with Tekton, you need to create a TaskRun, which is another Kubernetes object used to specify run time information for a Task.

To view this TaskRun object you can run the following Tekton CLI (tkn) command:

```bash
tkn task start hello --dry-run
```

After running the command above, the following TaskRun definition should be shown:

```yaml
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  generateName: hello-run-
spec:
  taskRef:
    name: hello
```

To use the TaskRun above to start the hello Task, you can either use tkn or kubectl.

Start with tkn:

```bash
tkn task start hello
```

Start with kubectl:

```bash
# use tkn's --dry-run option to save the TaskRun to a file
tkn task start hello --dry-run > taskRun-hello.yaml
# create the TaskRun
kubectl create -f taskRun-hello.yaml
```

Tekton will now start running your Task. To see the logs of the last TaskRun, run the following tkn command:

```bash
tkn taskrun logs --last -f
```

It may take a few moments before your Task completes. When it executes, it should show the following output:

```text
[hello] Hello World!
```

## Create a second basic Task

In this section, we will build upon the first task we created and create a second task and verify it. It may seem repeatitive, but this is just an example. (after you're done just imagine what you could do!)

### Extending your first CI/CD Workflow with a second Task and a Pipeline

As you learned previously, with Tekton, each operation in your `CI/CD` workflow becomes a `Step`, which is executed with a container image you specify. `Steps` are then organized in `Tasks`, which run as a Kubernetes pod in your cluster. You can further organize `Tasks` into `Pipelines`, which can control the order of execution of several `Tasks`.

To create a second `Task`, create a Kubernetes object using the Tekton API with the kind `Task`. The following YAML file specifies a `Task` with one simple `Step`, which prints a `Goodbye World!` message using the official Ubuntu image:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: goodbye
spec:
  steps:
    - name: goodbye
      image: ubuntu
      script: |
        set -e
        echo "Goodbye World!"
```

Write the YAML above to a file named `task-goodbye.yaml`, and apply it to your Kubernetes cluster:

```bash
kubectl apply -f task-goodbye.yaml
```

To run this task with Tekton, you need to create a `TaskRun`, which is another Kubernetes object used to specify run time information for a `Task`.

To view this `TaskRun` object you can run the following Tekton CLI (`tkn`) command:

```bash
tkn task start goodbye --dry-run
```

After running the command above, the following `TaskRun` definition should be shown:

```yaml
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  generateName: goodbye-run-
spec:
  taskRef:
    name: goodbye
```

To use the `TaskRun` above to start the `echo` `Task`, you can either use `tkn` or `kubectl`.

Start with `tkn`:

```bash
tkn task start goodbye
```

Start with `kubectl`:

```bash
# use tkn's --dry-run option to save the TaskRun to a file
tkn task start goodbye --dry-run > taskRun-goodbye.yaml
# create the TaskRun
kubectl create -f taskRun-goodbye.yaml
```

Tekton will now start running your `Task`. To see the logs of the `TaskRun`, run the following `tkn` command:

```bash
tkn taskrun logs --last -f
```

It may take a few moments before your `Task` completes. When it executes, it should show the following output:

```text
[goodbye] Goodbye World!
```

## Create a Pipeline and PipelineRun

In this section, we will create the pipeline combining the two tasks.

To create a `Pipeline`, create a Kubernetes object using the Tekton API with the kind `Pipeline`. The following YAML file specifies a `Pipeline`.

```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: hello-goodbye
spec:
  tasks:
  - name: hello
    taskRef:
      name: hello
  - name: goodbye
    runAfter: 
      - hello
    taskRef:
      name: goodbye
```

Write the YAML above to a file named `pipeline-hello-goodbye.yaml`, and apply it to your Kubernetes cluster:

```bash
kubectl apply -f pipeline-hello-goodbye.yaml
```

To run this pipeline with Tekton, you need to create a `pipelineRun`, which is another Kubernetes object used to specify run time information for a `Pipeline`.

To view this `pipelineRun` object you can run the following Tekton CLI (`tkn`) command:

```bash
tkn pipeline start hello-goodbye --dry-run
```

After running the command above, the following `PipelineRun` definition should be shown:

```yaml
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  generateName: hello-goodbye-run-
spec:
  pipelineRef:
    name: hello-goodbye
```

To use the `pipelineRun` above to start the `echo` `Pipeline`, you can either use `tkn` or `kubectl`.

Start with `tkn`:

```bash
tkn pipeline start hello-goodbye
```

Start with `kubectl`:

```bash
# use tkn's --dry-run option to save the pipelineRun to a file
tkn pipeline start hello-goodbye --dry-run > pipelineRun-hello-goodbye.yaml
# create the pipelineRun
kubectl create -f pipelineRun-hello-goodbye.yaml
```

Tekton will now start running your `Pipeline`. To see the logs of the `pipelineRun`, run the following `tkn` command:

```bash
tkn pipelinerun logs --last -f
```

It may take a few moments before your Pipeline completes. When it executes, it should show the following output:

```text
[hello : hello] Hello World!
[hello : hello] + set -e
[hello : hello] + echo Hello World!

[goodbye : goodbye] Goodbye World!
[goodbye : goodbye] + set -e
[goodbye : goodbye] + echo Goodbye World!
```
