Camera
=======================


## Hardware

We use the USB-3 Basler camera a2a3840-45umPRO to generate the recordings.
    
## Software


We use [baslerpi](https://github.com/shaliulab/baslerpi) to interact with the cameras and `ffmpeg` to save the video data in a memory efficient format.

`baslerpi` is a wrapper library around `pypylon`, the Python module produced by Basler (the camera supplier) to drive the cameras.
