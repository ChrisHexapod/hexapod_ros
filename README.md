# ROS Hexapod Stack (Forked)


This is a fork of the original Hexpod-ROS project by Kevin M. Ochs et al. (https://github.com/KevinOchs/hexapod_ros). Please follow his guide for an initial installation.

The original project was developed based on ROS Indigo targeted at Ubuntu 14.04, Raspberry Pi2 or ODroid.

With this fork the original project is ported to ROS Noetic on Ubuntu 20.04 LTS (Server Edition) running on a RaspberryPi 4 (4GB).  


## 1. Hardware

The project makes use of a 

* PhantomX Mark III
  * The ArbotixM Board was replaced by a U2D2, a USB communication converter. Please make sure that there is enough space to the upper deck.  
  * Since the U2D2 has only one ttl-level port you either need a U2D2 PowerHub, or the old 6 port hub (in addition to the PhantomX Hub).
  * Since connectors have changed an adapter cable is needed too.
  * You also have to think about power supply for your RaspberryPi. Here an y-cable, a 5V,3A BEC and a spare USB-C connector were used.
* Sensors
  * IMU: MPU2955
  * DepthSensor: Orbbec Astra Camera
* Controller
  * XBox360 Wireless

## 2. Installation

In addition to the ROS packages mentioned in the original project (since we switched from  indigo to noetic) you also need:

* ROS MPU9255 Node by Mauricio Leiton Lázaro
  *  URL: https://github.com/mdleiton/MPU9255
  *  Since this is an I2C sensor you need to have I2C activated on your Pi and you have to install the WiringPi library too (https://github.com/wbeebe/WiringPi).
  *  Ignore warnings regarding naming conventions
* imu_calib Node by Daniel Koch (orig) and Juan Miguel Jimeno (fork)
  * https://github.com/dpkoch/imu_calib or https://github.com/ChrisHexapod/imu_calib.git
  * Please run do_calib first to get the correct calibration data for your system
  * Please check topics or use my fork
* Astra Camera Node
  * http://wiki.ros.org/astra_camera  
* XBox Driver
  * sudo apt-get install xboxdrv  
  

## 3. Compiling

The orignal instruction asks to use a number of compiler options in order to optimize the code. However, since we are using an RPI4 on a 64Bit Ubuntu, we do not need all of them.

Please use: -march=armv8-a+crc -mcpu=cortex-a72 -mtune=cortex-a72

## 4. Assumptions / Notes

Since we are using an Ubuntu server image, we cannot start any GUI applications on the PI. Therefore launch files have been split to robot specific ones and those that should be started on a GUI device. The easiest way is to clone the repo to a remote computer and use:

* RPI
  * roslaunch hexapod_bringup hexapod_simple.launch (Locomotion only, no navigation) or
  * roslaunch hexapod_bringup hexapod_pi.launch (Full stack adapted to the new sensors)
* Remote Computer
  * roslaunch hexapod_bringup rviz.launch

The original PhantomX Model in this stack assumed two servos (pan & tilt) for the camera. In my case the camera is mounted directly to the hexyapod body. Therefore I reduced the number of servos (NUMBER_OF_HEAD_SEGMENTS: 0) in the phantomX.yaml file (params) and set the link type to "fixed" in the URDF description.

## 5. Troubleshooting

* If your hexapod acts like in slow-motion please check if you have specified the correct id's in phantomX.yaml. The original phantomX.yaml file specifies two additional ax12 for a camera gimbal and the ID of another ax12a was changed to 19 (instead of 1). The phantomX.yaml file in this branch uses the ID's as given in the PhantomX mark III assembly instructions and the camera gimbal has been removed.

* The MPU9255 was written some time ago and is not really adapted towards tf2. So if you are getting error mesages that contain "....at line 134 in /tmp/binarydeb/ros-noetic-tf2-0.7.5/src/buffer_core.cpp..." you have to change line 42 in MPU9255_node.cpp from: "data_imu.header.frame_id = "/imu_link";" to "data_imu.header.frame_id = "imu_link"

## 6. Things to Do

* Upgrade the Dynamixel SDK from 3.6.0 to 3.7.31

## 7. Pics

Top-View (no camera)

![IMG_20220210_112945502](https://user-images.githubusercontent.com/97293339/153389677-666551e6-4639-4c3a-8491-f92fc7495599.jpg)

Camera

![IMG_20220217_124609279](https://user-images.githubusercontent.com/97293339/154476293-675372ba-2e4e-4e88-b942-c93cfa35d6fd.jpg)

Middle-Deck (U2D2)

![IMG_20220217_124609279](https://user-images.githubusercontent.com/97293339/154476051-80a34afc-d07a-4283-adb7-8de5d970bb75.jpg)


TF-Tree
![frames](https://user-images.githubusercontent.com/97293339/154475328-af050dba-d370-46c5-b245-3f1450307a61.png)

