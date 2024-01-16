# Stable Diffusion

DeepSquare integrates the neural network text-to-image model, `Stable Diffusion`.

This guide illustrates how we designed and implemented the workflow to execute Stable Diffusion on the DeepSquare Grid.

[Click here](https://docs.deepsquare.run/workflow/samples/stable-diffusion) to know more about the Stable-diffusion workflow in the documentation.

## Usage

Replace the variables environment and submit the job. A "transfer.deepsquare.run" will be temporarily available in the logs to extract the output.

## Design

We designed the workflow as follows:

- The prompt is sent over an environment variable.
- Most of the parameters are sent via environment variables.
- Images are sent to <https://transfer.deepsquare.run/>

The docker image is already compiled from `github.com/Stability-AI/stablediffusion` and is exported as `registry-1.deepsquare.run/library/stable-diffusion:latest`.

The steps are as follows:

- Inference loop: generate the images. Rows are distributed into task per GPU.
- Combine all the images into one grid.

## Implementation

Let's start with the input, output and resources. For this application we decided to run 4 parallel tasks. Each one has 8 CPUs, 8 GB of RAM and 1 GPU.

### Inference loop

We just need to execute a `for` directive which executes 4 steps in parallel.

DeepSquare already hosts its own models at `/opt/models`. If you plan to use your own model, you should import the model using the input directive.

The last step is to assemble the rows into a grid.

### Combine the rows

Our docker image already includes ImageMagick, meaning we can compose a new image from the generated images.

We send the "grid" image to <https://transfer.deepsquare.run/>. The output directory contains all the images in their original resolution, which will be sent to <https://transfer.deepsquare.run/>.

## Conclusion

We have developed an ML inference workflow. Most inference processes with an output will follow the same pattern:

- Launch the inference in parallel
- Reassemble the output
