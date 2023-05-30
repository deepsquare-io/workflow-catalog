# Hello World Workflow

## Understanding the Workflow File

The workflow file is composed of several sections. Here's what each section means:

- **resources**: This section defines the resources that will be allocated for running this workflow. Here's what each field in the resources section means:

  - **tasks**: This parameter specifies the number of tasks to be launched for the job. A task is a logical unit of work, an instance of the computation you want to perform, and is executed as an isolated process. In this context, each task has its own allocated resources as specified in the workflow file, and can run independently or communicate with other tasks if necessary (for example, in parallel computing applications). By specifying `tasks: 1`, the workflow will run a single instance of the command specified in the `steps`.

  - **gpusPerTask**: This indicates how many GPUs will be allocated per task. In this case, it's 0, which means we're not using any GPUs for this task.
  - **cpusPerTask**: This indicates how many CPUs will be allocated per task. In this case, it's 1, which means we're allocating one CPU per task.
  - **memPerCpu**: This specifies how much memory (in MB) will be allocated per CPU. In this case, it's 1024 MB, which is the amount of memory allocated for the CPU executing the task.

- **enableLogging**: If set to true, this allows the application to send logs to the DeepSquare logging system. This can be helpful for debugging or tracking the execution status of the tasks.

- **steps**: This is a list of steps that will be run. Each step has a name and a command to run. The command can be any shell command. In this case, we're running the command `echo "Hello World"`. This command simply outputs the text "Hello World" to the console.

Each step is executed using the environment with the resources specified in the "resources" section. So, in this example, the "Hello World" command will run as a single task using one CPU and 1024 MB of memory.

That's it! This workflow file would tell DeepSquare to print "Hello World" to the console in an environment with the specified resources.
