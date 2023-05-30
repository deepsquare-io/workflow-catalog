# Blender Workflow

DeepSquare integrates the open-source 3D creation suite, Blender, for generating visual effects, animated films, 3D models, and more.

This guide provides a summary of how we designed and implemented the workflow to run Blender on the DeepSquare Grid.

## Design

We structured the workflow as follows:

- The rendering task is partitioned into several parallel tasks.
- The output is delivered as images or video.
- The docker image is compiled from `github.com/linuxserver/docker-blender` and exported as `docker.io/linuxserver/blender`.

The steps include:

1.  Calculation of the total number of frames and their even distribution.
2.  Parallel rendering of the frames.
3.  Combination of the frames or videos.

## Implementation

We use 4 parallel tasks, with each task having 8 CPUs, 8 GB of RAM, and 1 GPU.

### Compute the Number of Frames

The first step involves calculating the number of frames. We use Python scripts and Blender's Python API to obtain details about the frame range and calculate the number of frames per task.

### Render the Frames

The second step is rendering the frames. We use a `for` directive and the variable `$index` to select and render the corresponding frames in parallel.

For every sub-step, we calculate the start and end frame indexes and then render those frames with Blender in command-line mode. We use the CYCLES render engine and the OPTIX device for rendering. The rendered frames are saved in the OPEN_EXR format.

At the end of this step, each task will have rendered a portion of the total frames.

## Conclusion

This Blender workflow on the DeepSquare Grid allows for efficient rendering of complex 3D models by distributing the load across multiple tasks. This approach harnesses the power of parallel computing to reduce the overall rendering time, making it an ideal solution for large scale 3D rendering tasks.
