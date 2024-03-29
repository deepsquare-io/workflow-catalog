# Image Upscaling

DeepSquare integrates the neural network model optimised image upscaler, `Real-ESRGAN`. This guide illustrates the workflow design and implementation for executing Real-ESRGAN on the DeepSquare Grid.

[Click here](https://docs.deepsquare.run/workflow/samples/upscaling) to know more about the Image Uspcaling workflow in the documentation.

## Usage

Edit the "S3" fields. The S3 bucket must contain a video or images.

Edit the environment variable to customize the behavior of the job.

## Workflow Design

The workflow design is as follows:

- The input can be an image or a video.
- If the input is a video, the frames are extracted.
- The extracted images are distributed evenly among the GPUs.
- The scaled frames are reassembled into the original video.
- The output will be the scaled image or video.

The Docker image, compiled from [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN), is already exported as `registry-1.deepsquare.run/library/upscaling:latest`.

The workflow steps include:

1. Compute the number of images (extract and distribute the frames into batches if the input is a video).
2. Upscaling of the images.
3. If the input is a video, reassemble the images into a video.

## Workflow Implementation

### Compute the number of frames

The first step in our workflow is to compute the number of frames.

The script uses the `file -i` command to display the `MIME` type and filters out all files that are not videos or images. The images are then extracted and stored in the `input_frames` directory. Finally, we calculate the number of images and distribute them to the tasks.

### Upscale the frames

In the second step, we upscale the frames. We launch multiple substeps in parallel, using the `for` directive and the variable `$index` to select the batch directory.

After executing the `upscale.sh` script, the frames will be generated inside the output_frames directory.

### Re-assemble the frames

If the input was a video, we reassemble all the frames into a new video stream:

Using `ffmpeg`, we can determine the FPS of the original video and create a new video with the upscaled frames.

## Conclusion

We've developed this workflow following a similar pattern to Blender:

Divide the data into tasks
Execute a for loop that runs one task per GPU
Reassemble the output
This allows for efficient processing and rendering of both images
