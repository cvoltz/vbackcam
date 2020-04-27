# Description

[Benjamin
Elder](https://github.com/BenTheElder?after=Y3Vyc29yOnYyOpK5MjAxNC0wNi0wN1QxMjoxNzo0MC0wNTowMM4BOmBv&tab=repositories)
published the great article *[Open Source Virtual
Background](https://elder.dev/posts/open-source-virtual-background/)* which
explained how to create a camera feed with a virtual background for use in
conferencing applications. While the article itself is published
[here](https://github.com/BenTheElder/site/blob/master/content/posts/open-source-virtual-background.md)
on GitHub, unfortunately, the code itself wasn't gathered together in a
repository to make it easy for others to use. Additionally, the article was
written for a Debian derivative. My machines run Fedora and CentOS so I put
together this repository to make it easier for people running Fedora and CentOS
to be able to replicate Ben's work.

## Notes

* TCP port 9000 is used to connect the container running bodypix to the container
running the fake camera over a bridged network which is automatically created.
* The camera output is limited (to improve performance) to 1280x720.
* The containers used are named `bodypix` and `fakecam`.

# Requirements

* Fedora 31 or CentOS 7.7
* Docker CE 19.03.8
* Optional: NVIDIA graphics card with [CUDA
  support](https://developer.nvidia.com/cuda-gpus), for faster inference
  * [NVIDIA GPU drivers](https://www.nvidia.com/drivers) 418.x or later
  * [CUDA toolkit](https://developer.nvidia.com/cuda-toolkit-archive) 10.1

# Install

1. Clone the repository into `fakecam` directory:
   ```bash
   git clone ... fakecam
   cd fakecam
   ```
1. Run `setup`:
   ```bash
   ./setup
   ```
1. Copy the image you want to use to `fakecam/background.jpg`. For example:
   ```bash
   cp backgrounds/star-wars-feature-vf-2019-summer-embed-07.jpg \
     fakecam/background.jpg
   ```
1. Build the Docker images:
   ```bash
   ./build
   ```

# Use

Run `vbackcam` to start and stop the fake camera with the virtual background.

While the fake camera is running, open your conferencing application and select
`v4l2loopback` or `/dev/video20` as the camera.

## Change the background

1. Copy the new background image into `fakecam/background.jpg`
2. Rebuild the `fakecam` Docker image:
   ```
   docker build --tag fakecam ./fakecam
   ```

# Useful links

* *[Add kernel modules with
  DKMS](https://docs.01.org/clearlinux/latest/guides/kernel/kernel-modules-dkms.html)*
* Backgrounds:
  * [Star Wars: The Rise of Skywalker
    Photos](https://www.vanityfair.com/hollywood/photos/2019/05/star-wars-the-rise-of-skywalker-exclusive-photos)
  * [TrekCore.com Gallery](https://tos.trekcore.com/gallery)
  * [Unsplash](https://unsplash.com): The internet's source of freely usable images
* [BodyPix](https://blog.tensorflow.org/2019/11/updated-bodypix-2.html):
  Real-time Person Segmentation in the Brower with TensorFlow.js
  * [BodyPix
    repository](https://github.com/tensorflow/tfjs-models/tree/master/body-pix)
  * [body-pix npm](https://www.npmjs.com/package/body-pix-node)
* [Docker Engine](https://docs.docker.com/engine)
  * *[Install Docker Engine on
    CentOS](https://docs.docker.com/engine/install/centos/)*
  * *[Install Docker Engine on
    Fedora](https://docs.docker.com/engine/install/fedora/)*
* [node.js](https://nodejs.org/en/)
* NVIDIA
  * [CUDA enabled GPUs](https://developer.nvidia.com/cuda-gpus)
  * [CUDA toolkit](https://developer.nvidia.com/cuda-toolkit)
  * [cuDNN](https://developer.nvidia.com/cudnn): CUDA Deep Neural Network library
  * [GPU drivers](https://www.nvidia.com/drivers)
  * [nvidia-docker](https://github.com/NVIDIA/nvidia-docker): Build and run
    Docker containers leveraging NVIDIA GPUs
* *[Open Source Virtual
  Background](https://elder.dev/posts/open-source-virtual-background/)*
* [OpenCV python bindings](https://pypi.org/project/opencv-python/)
* [pyfakewebcam](https://github.com/jremmons/pyfakewebcam): A library for writing
  RGB frames to a fake webcam device on Linux
* [TensorFlow](https://www.tensorflow.org/): Open source library to help deliver
  and train ML models
  * [TensorFlow GPU support](https://www.tensorflow.org/install/gpu)
  * [TensorFlow.js](https://www.tensorflow.org/js): A library for machine
    learning in JavaScript
* [Video for Linux Two (V4L2)](https://en.wikipedia.org/wiki/Video4Linux)
  * [Linux TV](https://www.linuxtv.org/)
    * *[Part I - Video for Linux
      API](https://www.linuxtv.org/downloads/v4l-dvb-apis-new/userspace-api/v4l/v4l2.html)*
  * [v4l2loopback](https://github.com/umlaeute/v4l2loopback): A kernel module to
    create V4L2 loopback devices
  * [v4l2ucp](https://sourceforge.net/projects/v4l2ucp/): Universal control
    panel for Video for Linux Two (V4L2) devices

# License

Photo copyrights:
  * Annie Leibovitz or [Vanity Fair](https://www.vanityfair.com)/[Condé Nast](https://www.condenast.com)
  * [Dorsa
    Masghati](https://unsplash.com/@dorsamasghati?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on  [Unsplash
    wallpapers](https://unsplash.com/t/wallpapers?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
  * [Moosa
    Haleem](https://unsplash.com/@moseshalym?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [Unsplash
    wallpapers](https://unsplash.com/t/wallpapers?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
  * [Nastuh
    Abootalebi](https://unsplash.com/@sunday_digital?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [Unsplash
    interiors](https://unsplash.com/t/interiors?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
  * [TrekCore.com](https://tos.trekcore.com)

Copyright © 2020 [Christopher Voltz](mailto:cjunk@voltz.us)

This package is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation; either version 2 of the License, or (at your option) any later
version.

This package is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
this program. If not, see http://www.gnu.org/licenses/.
