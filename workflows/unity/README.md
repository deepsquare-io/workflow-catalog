# Unity Render Streaming Workflow

Unity Render Streaming is a solution for peer-to-peer streaming that uses `WebRTC` for `NAT traversal` via `STUN`, thereby eliminating the need for a tunnel to expose the video stream.

[Click here](https://docs.deepsquare.run/workflow/samples/unity-render-streaming) to know more about the Unity Render Streaming workflow in the documentation.

## Design

A graphical session can be run inside a container with the following conditions:

- Mount an x11 socket
- Set a x11 DISPLAY via the DISPLAY environment variable
- Ensure the container has all the necessary shared libraries to run an x11 session.
- The required shared libraries include libglvnd0, libgl1, libglx0, libegl1, libgles2, libxcb1-dev, libx11-xcb-dev, libglib2.0-0, libc++1-10, mesa-utils, libx11-dev, libxkbcommon-dev, libwayland-dev, libxrandr-dev, libegl1-mesa-dev, vulkan-utils, libgl1-mesa-glx, libvulkan1, libvulkan-dev, ocl-icd-opencl-dev.

If Vulkan is being used inside your Unity application, the Vulkan SDK should also be installed. The DeepSquare Grid should already mount the devices and shared libraries of the NVIDIA drivers.

Please note that since this is not an HPC workload, parallel computing is not possible. The service can only run with a `single GPU`, as there is no parallel decomposition. The application simply runs in one step: "Run the application".
