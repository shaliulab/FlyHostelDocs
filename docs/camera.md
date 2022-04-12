Camera
=======================

## Hardware

We use the USB-3 Basler camera a2a3840-45umPRO to generate the recordings. A [profile file for this camera](assets/a2A3840-45umPRO.pfs) can be used to replicate the camera configuration. This camera can deliver up to 45 FPS at 6MP resolution. We record at 40 FPS and crop a square ROI out of the sensor feed, which is rectangular (3860x2178). The square is rougly 2000x2000 (4MP)

We also use the Chameleon3 CM3-U3-13Y3C (Flir) as a backup camera at 100 FPS and 10 ms exposure to capture very fast behavior that automated AI cannot process, but a human can resolve.
Eventually we will switch to cameras from a single supplier, probably Basler only.


## Software

We use [scicam](https://github.com/shaliulab/scicam) to interact with the cameras and `ffmpeg` to save the video data in a memory efficient format.

`scicam` is a wrapper library around `pypylon`, the Python module produced by Basler (the camera supplier) to drive Basler cameras, and `simple_pyspin`, the analagous package for Flir cameras.


scicam is called as follows

```
scicam --cameras Flir Basler --flir-exposure 9900 --flir-framerate 100 --basler-exposure 24000 --basler-framerate 40 --sensor 192.168.0.103:9000 --chunk-duration 300 --select-rois
```

* `--cameras` selects both the high-resolution and lower speed Basler camera and the lower-resolution but very high speed Flir camera
* `--flir-exposure --flir-framerate --basler-exposure --basler-exposure` set the framerate and exposure time of the cameras
* `--sensor` contains the IP address and port of a sensor server that returns a JSON with fields `temperature` `humidity` and `light`, as explained in the [sensor](sensor.md) page.
* `--chunk-duration` is a number in seconds that states how long each imgstore chunk will be (300 seconds = 5 mins).
* `--select-rois` prompts a GUI that allows users to select the ROI for each camera feed, that way non relevant parts of the feed are not saved, which saves space.
