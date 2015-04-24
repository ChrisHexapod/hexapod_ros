ROS Hexapod Stack
=================
This is a work in progress of my implementation of a hexapod functioning in the ROS framework. It is still very much a work in progress and I am still actively developing it. Its current capabilities are up to 2D mapping its environment.

Author: Kevin M. Ochs

Contributor: Renée Love


Dependencies
------------

```
sudo apt-get install ros-indigo-sound-play
sudo apt-get install ros-indigo-diagnostic-updater
sudo apt-get install ros-indigo-xacro
sudo apt-get install ros-indigo-openni2-launch
sudo apt-get install ros-indigo-depthimage-to-laserscan
sudo apt-get install ros-indigo-joystick-drivers
sudo apt-get install ros-indigo-imu-filter-madgwick
sudo apt-get install libusb-1.0-0-dev
```

_Joystick_
----------

For pairing a PS3 controller you can either install BlueZ5 or follow the below link.

https://help.ubuntu.com/community/Sixaxis

Install
-------

```
git clone https://github.com/KevinOchs/ROS_hexapod.git
```

For PhantomX branch created by Renée Love:

```
git checkout PhantomX
```

Pictures
--------
Rviz screenshot of point cloud and laserscan active.
![ScreenShot](http://forums.trossenrobotics.com/gallery/files/8/6/6/6/depthwithlaser.jpg)

2D room mapping in Rviz.
![ScreenShot](http://forums.trossenrobotics.com/gallery/files/8/6/6/6/2d_slam.jpg)

Renée Love's adaptation of the Hexapod stack for Trossen's  [PhantomX](http://www.trossenrobotics.com/phantomx-ax-hexapod.aspx).
![ScreenShot](http://forums.trossenrobotics.com/gallery/files/1/2/6/6/9/screenshot_from_2015-04-22_20_23_15.png)


Videos 
------
_Click on picture for redirect to YouTube video._

Small video of Golem research platform and IMU testing. 
[![ScreenShot](http://img.youtube.com/vi/IP-1HebkZnU/0.jpg)](https://www.youtube.com/watch?v=IP-1HebkZnU)

Renée Love's odometry test video using the phantomX.
[![ScreenShot](http://img.youtube.com/vi/VYBAM0MrvWI/0.jpg)](https://www.youtube.com/watch?v=VYBAM0MrvWI)