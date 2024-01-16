# Unity Render Streaming Workflow

Unity Render Streaming is a solution for peer-to-peer streaming that uses `WebRTC` for `NAT traversal` via `STUN`, thereby eliminating the need for a tunnel to expose the video stream.

[Click here](https://docs.deepsquare.run/workflow/samples/unity-render-streaming) to know more about the Unity Render Streaming workflow in the documentation.

## Usage

The usage is very application specific.

1. Develop a Unity application with [Unity Render Streaming](https://docs.unity3d.com/Packages/com.unity.renderstreaming@3.1/manual/index.html).
2. Host the web application on the cloud.
3. Edit the job and pass the web application server URL to your Unity application.
4. Submit the job and use the web application server to interact with the Unity application.

## Design

A graphical session can be run inside a container with the following conditions:

- Mount a x11 socket
- Set a x11 DISPLAY via the DISPLAY environment variable
- Ensure the container has all the necessary shared libraries to run an x11 session.
- The required shared libraries include libglvnd0, libgl1, libglx0, libegl1, libgles2, libxcb1-dev, libx11-xcb-dev, libglib2.0-0, libc++1-10, mesa-utils, libx11-dev, libxkbcommon-dev, libwayland-dev, libxrandr-dev, libegl1-mesa-dev, vulkan-utils, libgl1-mesa-glx, libvulkan1, libvulkan-dev, ocl-icd-opencl-dev.

If Vulkan is being used inside your Unity application, the Vulkan SDK should also be installed. The DeepSquare Grid should already mount the devices and shared libraries of the NVIDIA drivers.

Please note that since this is not an HPC workload, parallel computing is not possible. The service can only run with a `single GPU`, as there is no parallel decomposition. The application simply runs in one step: "Run the application".
