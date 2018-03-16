# Workflow File

In order to define your workflow, you can use a `YAML` formatted file that describes all your needs.

This file need to contains a [source event](../source.md) and one or multiple [tasks](../task.md)

[include](./example.yml)

You can find the raw file example <a href="./example.yml" target="_blank">here</a>

## Note on the parameters

#### Parameter type

Parameters needs to be send with the right type (Number, String, Object, Array, Boolean) according to the documentation of the service.

#### Parameter binding

Every parameters can be binded to a dynamic value or from the workflow execution or the workflow deployment. Here are the following syntaxes to achieve this.

##### Workflow variables

Your workflow will need to access variable from the event or some other steps from the workflow. In order to do that you can refer the result directly from your template. The value will be applied during the processing of the workflow.

With the worfklow variables you can have access to the **inputs** of the workflow, the **source** event data or any **task** result 

```yaml
source:
  service: Ethereum
  ...
...
tasks:
  processAmount:
    ...
    parameters:
      amount: ${workflow:source.amount}
  notify:
    ...
    parameters:
      title: ${workflow:inputs.notificationTitle}
      value: ${workflow:processAmount.result}
inputs:
  notificationTitle: "Title for the notification"
```

##### Environment variables

In many case you don't need to write some private data on the file, in case you want to use a versioning system, if you want to have different environments etc... In this case you can use environmental variables. The value will be replace when the workflow is deployed

```yaml
...
tasks:
  xxx:
    ...
    parameters:
      secret: ${env:SECRET}
```

##### Default value

You might need to have some default value in case the variable are not present during the deployment or the processing. In order to do that you can give another argument to the template

```yaml
parameterX: ${env:PARAMETER_X, 42}
```

## Task processing

If your workflow contains multiple tasks to execute, the {{ book.network }} will automatically optimise the workflow to parallelise the tasks. In order to parallelise the execution, a dependency graph will be generated with the source event as a root node and for parallelise all the child with the same depth.

#### Instant tasks

If a task doesn't have a direct or indirect dependency to the event, this task will be executed from your computer while deploying and will not be executed everytime the workflow starts but will use the value from the result during the deployment.

#### Concurrency

Because of the parralelisation of the task it is not guarantee to have an task executed before another one if they don't have any dependencies. If you want to ensure that a task run after another one you need to create a [workflow variable](#workflow-variables) from this task.

#### Cycles

Because of the dependency generation your workflow cannot contain two task that depends to each others (even through different depths). If you have a cycle in your workflow, you will have an error while validating or deploying.