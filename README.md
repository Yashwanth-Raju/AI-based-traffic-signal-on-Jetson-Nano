
# AI based Traffic signal

This repository is for a AI based traffic signal designed to improve pedestrian safety. Using a camera, the system detects pedestrians at zebra crossings and adjusts traffic signals accordingly. It can be seamlessly integrated with existing traffic control infrastructure to enhance functionality.

The primary goal is to alert vehicles approaching a zebra crossing when a pedestrian is present. This system is particularly beneficial in low-visibility conditions, such as at night, ensuring that drivers are aware of pedestrians on the road

This system controls three signals for each lane: Vehicle Red, Vehicle Green, and Pedestrian Green.

Each lane is divided into three zones: Waiting Area 1, Main Area, and Waiting Area 2. If a pedestrian is detected in either Waiting Area 1 or Waiting Area 2, both the pedestrian green signal and the vehicle green signal will blink at a set frequency. This blinking acts as a warning to both the pedestrian and the driver, indicating a potential crossing.

When the pedestrian enters the Main Area, the pedestrian signal turns solid green, allowing them to cross safely, while the vehicle signal turns red, instructing the driver to stop before the zebra crossing. Once the pedestrian crosses, the vehicle signal turns green again, and the pedestrian signal turns off, allowing vehicles to resume movement

## Device set up
### Step 1
Just follow this -> [Get Started With Jetson Nano Developer Kit](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#intro) on your Jetson device. 


### Step 2

To build and install jetson-inference, see [this page](https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md) or run below commands on your jetson device once setup is done:

```bash
cd ~
sudo apt-get install git cmake
git clone --recursive https://github.com/dusty-nv/jetson-inference
cd jetson-inference
mkdir build
cd build
cmake ../
make -j$(nproc)
sudo make install
sudo ldconfig
```


Test it here -> [Classifying Images with ImageNet](https://github.com/dusty-nv/jetson-inference/blob/master/docs/imagenet-console-2.md)

### Step 3

Library Installation

```bash
sudo pip install Jetson.GPIO
pip install --user numpy
pip install --user jetson-utils
pip install --user opencv-python
```
All set!

### Step 4



Position the cameras at the desired locations where the lane is clearly visible. Capture a frame from the camera feed and save it to a local directory. This frame will be used to define the region of interest (ROI) for monitoring pedestrian activity

#### Frame capture 


Run -> [frame_capture.py](https://github.com/Yashwanth-Raju/AI-based-traffic-signal-on-Jetson-Nano/blob/main/frame%20_capture.py)

```bash
python3 frame_capture.py
```

press 'x' to capture a frame

The frame is then stored into the current working directory.

#### Defining region & getting coordinates

Run -> [region_define.py](https://github.com/Yashwanth-Raju/AI-based-traffic-signal-on-Jetson-Nano/blob/main/region_define.py)

```bash
python3 region_define.py
```

Click on the window to get the coordinates of the region.

Top left is (0,0) & bottom right is (x,y)

update the coordinates in the [main.py](https://github.com/Yashwanth-Raju/AI-based-traffic-signal-on-Jetson-Nano/blob/main/main.py)

### Step 5

#### Final command

```bash
python3 main.py 
```



