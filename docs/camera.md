# Camera

## Hardware

We use the USB-3 Basler [a2A1920-160umBAS](https://www.baslerweb.com/en/products/cameras/area-scan-cameras/ace2/a2a1920-160umbas/) with [Basler Lens C11-2520-12M-P f25mm ](https://www.baslerweb.com/en/products/lenses/fixed-focal-lenses/basler-lens-c11-2520-12m-p-f25mm) to generate the vide recordings. A [profile file for this camera](assets/a2A1920-160umBAS.pfs) can be used to replicate the camera configuration. This camera can deliver up to 160 FPS at 2.3MP resolution. We record at 150 FPS and crop a square ROI out of the sensor feed, which is rectangular (1920x1200). The square is rougly 1000x1000 (1MP)

## Software

We use [scicam](https://github.com/shaliulab/scicam) to interact with the cameras and `ffmpeg` to save the video data in a memory efficient format.

`scicam` is a wrapper library around `pypylon`, the Python module produced by Basler (the camera supplier) to drive Basler cameras.

To install it: `pip install scicam==0.1.3`

scicam is called as follows

```bash
CUDA_VISIBLE_DEVICES=1; scicam --setup FlyHostel3 --chunk-duration 300 --start-time   1682604000 --sensor 192.168.0.103:9000  --X 1
```

`CUDA_VISIBLE_DEVICES=1` will make the GPU with ID 1 (as reported by `nvidia-smi`) to be in charge of efficiently encoding the video to `.mp4`.

```bash
nvidia-smi
```

```
Wed May  3 08:32:33 2023       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 525.105.17   Driver Version: 525.105.17   CUDA Version: 12.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:15:00.0 Off |                  N/A |
| 30%   27C    P8    15W / 350W |      6MiB / 24576MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA RTX A4000    Off  | 00000000:21:00.0  On |                  Off |
| 41%   30C    P8     9W / 140W |    488MiB / 16376MiB |      3%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
```

This output shows `CUDA_VISIBLE_DEVICES=1` will put the `NVIDIA RTX A4000` in charge. The advantage of this GPU is that its only limit on how many videos it can encode is its memory, and not the number of slots. The NVIDIA GeForce card actually has more RAM, but it can only take 3 videos simultaneously, even if they only took say half the memory. This is summarised in this table https://developer.nvidia.com/video-encode-and-decode-gpu-support-matrix-new#Encoder


* `--sensor` contains the URL (IP address and port) of a sensor server that returns a JSON with fields `temperature` `humidity`, `light` and `camera_light`, as explained in the [sensor](sensor.md) page.
* `--chunk-duration 300` is a number in seconds that states how long each imgstore chunk will be (300 seconds = 5 mins).
* `--select-rois` prompts a GUI that allows users to select the ROI for each camera feed, that way non relevant parts of the feed are not saved, which saves space.
* `--setup FlyHostel3` specifies which of the 4 setups to run. Options are `FlyHostel1 FlyHostel2 FlyHostel3 FlyHostel4`.
* `--X 1` number of animals in the experiment. This feature allows `scicam` to create the experiment data in the right X folder (a folder where all experiments have the same number of animals)
* `--start-time 1682604000` timestamp in seconds when the experiment started, in this case 2023-04-27 14:00:00.

Scicam uses a derived version of [imgstore](https://github.com/loopbio/imgstore) available under https://github.com/shaliulab/imgstore. See more in [imgstore](imgstore.md)