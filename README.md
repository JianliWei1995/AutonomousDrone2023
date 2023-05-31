# UAS Geotracking 2023

## Project Description
Compared with UAS geotracking project 2022, we have two updates:
- We applied drone mapping to generate aerial map to replace aerial orthophoto download from Google Earth. Aerial map constains most recent updates, furthermore enhance UAS geotraking pipeline robustness.
- When generated aerial map available, we replace SuperGlue feature matching scheme with ORB detector. ORB detector will reduce pipeline reliance on computer memory and accelerate pipeline running speed.

![demo_vid](https://github.com/OSUPCVLab/AutonomousDrone2023/blob/main/demo/UAV%20geotracking%20demo.gif)


## UAV test flight
Our test flight is at below area. The aerial mapping is collected with the Mavic Air 2. It most green and few buildings and road. Feel free to download them and run our demo.

<p>
  <img src="https://github.com/OSUPCVLab/AutonomousDrone2023/blob/main/premap/satmap.png" width=60% height=60% />
</p>


## Installation (Windows)
```shell
# Anaconda create a new environment
conda create -n UASGeotracking python=3.8
conda activate UASGeotracking

# Install required libraries, pytorch needs to be installed independently
cd AutonomousDrone2023
pip install -r requirements.txt
```
OpenCV cuda version installation on Windows, please refer to [Build OpenCV 4.4.0 with CUDA (GPU) Support on Windows 10](https://haroonshakeel.medium.com/build-opencv-4-4-0-with-cuda-gpu-support-on-windows-10-without-tears-aa85d470bcd0)


## Data to be download
We provide the [download link](https://buckeyemailosu-my.sharepoint.com/:f:/g/personal/wei_909_buckeyemail_osu_edu/Ete3t_9rVQlJmzF3hxr-NPEBZTR9R9jJ2JGknoYIk3CqBw?e=kg4inb) and saved files as following data structure
```
AutonomousDrone2023
├── input
    ├── images (~2.47GB, 612 sequential frames)
    └── videos
└── premap
    ├── satmap.png
    └── satmap_mask.npz
```

## Run the demo on a dictionary of images
```shell
# Running ORB-based UAS Geotracking with cuda acceleration
python run_orb.py --input=./input/images/ --output=./output/ --Orien=270 --Init_height=130 --range 900 --bin_interval=10 --matching_vis --semantic
```
- Use `--Orien` to preset UAV initial heading direction in reference to North direction countclockwisely
- Use `--Init_height` to preset UAV starting flight height (in meters)
- Use `--range` to predefine the width of look up region, valid only when `--Init_height` not provided
- Use `--Init_GPS` to preset UAV starting points, required for each flight
- Use `--semantic` to apply semantic building mask over matched features
- For more details, please refer to source code `run_orb.py` for more details
