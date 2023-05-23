# DeepSquare Workflows Repository

Welcome to the DeepSquare Workflows repository! This repository is dedicated to sharing workflows that help you get started with utilizing the DeepSquare infrastructure. Whether you are a developer, data scientist, or researcher, these workflows provide a streamlined way to run your applications and experiments on DeepSquare.

## Writing a Workflow File

A workflow file is a YAML file that describes the resource allocation and the set of instructions necessary to run your application on DeepSquare. To create a workflow file, you can follow these steps:

1. Start by containerizing your application, ensuring that it is compatible with DeepSquare.
2. Test your workflow on the DeepSquare Portal Dev App to verify its functionality.

## Understanding the Workflow Format

The workflow format consists of defining the resources allocated for your application and specifying the steps to run. Here is an example workflow in YAML format:

```yaml
resources:
  tasks: 16
  gpusPerTask: 0
  cpusPerTask: 1
  memPerCpu: 1024
enableLogging: true
steps:
  - name: run the application
    run:
      command: './main'
      workDir: '/app'
      resources:
        tasks: 16
      container:
        image: deepsquare-io/example:latest
        registry: ghcr.io
```

In this example, we allocate 16 tasks, with each task using 1 CPU and 1024 MB of RAM. The `enableLogging` parameter allows the application to send logs to the DeepSquare logging system for easy monitoring. The `steps` section defines the execution steps, including the command to run and the container image to use.

## Contributing

We welcome contributions from the community to expand the collection of workflows in this repository. By doing so, you help others get started and unlock the full potential of DeepSquare. If you would like to contribute a new workflow, please refer to the [contributing guidelines](CONTRIBUTING.md).

Thank you for using DeepSquare and being a part of our community!
