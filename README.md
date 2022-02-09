# ROS Hexapod Stack (Forked)


This is a fork of the original Hexpod-ROS project by Kevin M. Ochs et al. (https://github.com/KevinOchs/hexapod_ros). Please follow his guide for an initial installation.

The original project was developed based on ROS Indigo targeted at Ubuntu 14.04, Raspberry Pi2 or ODroid.

This fork has been ported to ROS-Noetic on Ubuntu 20.04 LTS running on a RaspberryPi 4 (4GB).

## 1. Hardware

The project makes use of a 

* PhantomX Mark III
  * The ArbotixM Board was replaced by a U2D2-Connector
  * For connecting all legs we also need a U2D2 PowerHub
  * Since connectors have changed an adapter cable is needed too
* Sensors
  * IMU: MPU2955
  * DepthSensor: Orbbec Astra Camera
* Controller
  * XBox360 Wireless

## 2. Compiling

The orignal instruction asks to use a number of compiler options in order to optimize the code. However, since we are using an RPI4 on a 64Bit Ubuntu, we do not need all of them.

Please use: -march=armv8-a+crc -mcpu=cortex-a72 -mtune=cortex-a72

## 3. Troubleshooting

If your hexapod acts like in slow-motion please check if you have specified the correct id's in phantomX.yaml. The origianl phantomX.yaml file specifies two additional ax12 for a camera gimabl and has changed the ID of one ax12a from 1 to 19. The phantomX.yaml file in this branch uses the ID's as given in the PhantomX mark III assembly instructions and the camera gimbal has been removed.

