markdown

# Go Chase It! Project

This project is part of the Udacity Robotics Software Engineer Nanodegree.

The goal of this project is to build a robot that can detect a white ball and chase it in a Gazebo simulation using ROS. The robot uses a camera image stream, processes the image to find the target, and then publishes movement commands so the robot can follow the ball.

## Project Overview

The project includes:

- A robot model launched in Gazebo
- ROS nodes for robot motion
- ROS nodes for image processing
- Communication through ROS topics between perception and motion components

The robot performs the following behavior:

1. Captures camera images
2. Detects the white ball in the image
3. Decides whether the ball is on the left, center, or right
4. Publishes velocity commands to move toward the ball

## Project Structure

```bash
catkin_ws/
├── src/
│   ├── ball_chaser/
│   │   ├── launch/
│   │   ├── src/
│   │   ├── CMakeLists.txt
│   │   └── package.xml
│   ├── my_robot/
│   │   ├── launch/
│   │   ├── urdf/
│   │   ├── worlds/
│   │   ├── CMakeLists.txt
│   │   └── package.xml
│   └── CMakeLists.txt
├── build/
└── devel/

Packages

my_robot

Contains the robot model, world files, and launch files needed to spawn the robot in Gazebo.

ball_chaser

Contains the ROS nodes responsible for:

    Driving the robot
    Processing camera images
    Detecting the white ball
    Sending movement commands

Requirements

    Ubuntu 20.04
    ROS Noetic
    Gazebo
    catkin workspace

Additional ROS packages may be required, such as:

bash

sudo apt update
sudo apt install ros-noetic-effort-controllers ros-noetic-ros-controllers ros-noetic-ros-control

Build Instructions

Clone the repository:

bash

git clone https://github.com/eljandoubi/catkin_ws.git
cd catkin_ws

Build the workspace:

bash

catkin_make

Source the workspace:

bash

source devel/setup.bash

How to Run

First, make sure ROS is sourced:

bash

source /opt/ros/noetic/setup.bash
source ~/catkin_ws/devel/setup.bash

Launch the robot world:

bash

roslaunch my_robot world.launch

In a new terminal, run the ball chaser node:

bash

rosrun ball_chaser drive_bot

In another terminal, run the image processing node:

bash

rosrun ball_chaser process_image

ROS Nodes

process_image

Subscribes to the robot camera topic, analyzes the image, and determines the position of the white ball.

drive_bot

Publishes velocity commands to move the robot left, right, or forward depending on the detected ball position.

Topics

Subscribed Topics

    /camera/rgb/image_raw — camera image stream

Published Topics

    /cmd_vel — robot velocity commands

Expected Behavior

When the simulation starts, the robot should detect the white ball and move toward it automatically.
If the ball appears:

    on the left, the robot turns left
    on the right, the robot turns right
    in the center, the robot moves forward

Notes

    Make sure all required ROS controller packages are installed.
    If Gazebo loads but the robot does not move, verify that the controllers are running correctly.
    If the workspace has permission issues, reset ownership with:

bash

sudo chown -R $USER:$USER ~/catkin_ws

Author