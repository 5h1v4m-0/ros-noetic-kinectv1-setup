
# Setup Kinect in ROS Noetic

This guide will walk you through the process of setting up Kinect in ROS Noetic


## Prerequisites

- Ubuntu 20.04

   ```bash
    lsb_release -a  #check ubuntu version
   ```
  ![Screenshot from 2024-03-13 16-30-56](https://github.com/5h1v4m-0/ros-noetic-kinectv1-setup/assets/99700035/586c59ec-9d29-469a-a443-7401c64cedb5)


- ROS Noetic installed ([installation instructions](http://wiki.ros.org/noetic/Installation))
  ```bash
  cd /opt/ros && ls #check ros distro
  ```
  ![Screenshot from 2024-03-13 16-41-35](https://github.com/5h1v4m-0/ros-noetic-kinectv1-setup/assets/99700035/2f59d81b-6be1-441f-bffd-183cfdfda13a)

- Kinect for Xbox 360 or Kinect for Windows (Kinect v1)

## Installation

1. **Update and upgrade.**:

 
   ```bash
   sudo apt update
   sudo apt upgrade
   ```
2. **Install Dependencies**
   ```bash
   sudo apt install ros-noetic-rgbd-launch
   sudo apt-get install ros-noetic-openni-launch
   sudo apt-get install libfreenect-dev
   ```
3. **Install Freenect**

   This package is not available in the official ROS Noetic repositories, so we need to clone the GitHub repository and build it. Follow these steps to do so.

   - Clone the package
     ```bash
     mkdir -p ~/catkin_ws/src
     cd ~/catkin_ws/src
     git clone https://github.com/ros-drivers/freenect_stack.git
     ```
   - Build Package
       ```bash
       cd ~/catkin_ws
       catkin_make
       source ~/catkin_ws/devel/setup.bash
       ```
 4. **Run the freenect launch file**
    - Always source the setup file
      ```bash
         source ~/catkin_ws/devel/setup.bash
      ```
    - connect the kinect_v1 to pc
      ```bash
        lsusb #list all conected device to pc
      ```
      Now, we will launch the freenect example for depth registration, which allows you to obtain the point cloud with RGB data superimposed over it.
      ```bash
      roslaunch freenect_launch freenect.launch depth_registration:=true
      ```
      visualize the topics from Kinect on Rviz, open a new terminal and launch rviz.
      ```bash
         rviz
      ```
      Now need to setup some parameters on rviz to visualize the depth registration data.
      1.  In the ‘Global Options’ set the ‘Fixed Frame’ to ‘camera_link’.
      2.  Add ‘pointcloud2’ object and set the topic to ‘/camera/depth_registered/points’
      
      ![Screenshot from 2024-03-13 17-21-21](https://github.com/5h1v4m-0/ros-noetic-kinectv1-setup/assets/99700035/899d2cdd-3280-4b56-834b-41ee46b90b92)

      Now wait for a few seconds to get the points on display!
  5. **Refrences**
     
     https://aibegins.net/2020/11/22/give-your-next-robot-3d-vision-kinect-v1-with-ros-noetic/
     
     http://www.choitek.com/uploads/5/0/8/4/50842795/ros_kinect.pdf
     
     http://wiki.ros.org/ROS/Tutorials/CreatingPackage
     
     https://naman5.wordpress.com/2014/06/24/experimenting-with-kinect-using-opencv-python-and-open-kinect-libfreenect/
     
      

      
    
