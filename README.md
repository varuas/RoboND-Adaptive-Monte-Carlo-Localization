# Adaptive Monte Carlo Localization using ROS and Gazebo

This project utilizes the ROS Adaptive Monte Carlo Localization (AMCL) package to accurately localize a mobile robot inside a map in a Gazebo simulation environment. The Robot has an RGB camera and a LIDAR sensor. It also utilizes odometry data on a simulated differential drive robot. AMCL dynamically adjusts the number of particles over a period of time, as the robot navigates around in a map. This adaptive process offers a significant computational advantage over MCL.

https://user-images.githubusercontent.com/3985351/162624309-16a2a6df-2d21-4fe3-a9d5-ee1d354f3df1.mp4

The above video shows the particle cloud when the robot is placed on a random position on the map. The teleop commands are used to move around the robot from there, and we can see the particles converging to the actual position as it takes in the LIDAR and odometry measurements.

Link to the full video: https://youtu.be/JKBZg4RiT9M

This project was developed as part of the Robotics Software Engineer Nanodegree from Udacity.


### Technologies & tools used
 - ROS Kinetic
 - Gazebo
 - ROS AMCL and Navigation stack
 - RViz
 - Unified Robot Description Format

### Robot Model Description
A differential drive robot (containing a chassis, two castor wheels, and two wheels) defined using the Unified Robot Description Format. It contains two sensors: a lidar and a camera. This project also uses Gazebo plugins for the robot’s differential drive, lidar, and camera.

### Pre-requisites

ROS Kinetic with the following packages:

    sudo apt-get install ros-kinetic-navigation
    sudo apt-get install ros-kinetic-map-server
    sudo apt-get install ros-kinetic-move-base
    sudo apt-get install ros-kinetic-amcl

Docker setup

    git clone https://github.com/jaismith/ros-apple-silicon
    docker-compose up --build
    docker-compose exec ros bash (docker-compose up has to be running)
    apt install ros-kinetic-desktop-full
    source /opt/ros/kinetic/setup.bash

Launch

    cd catkin_ws/
    roslaunch my_robot world.launch
    roslaunch my_robot amcl.launch


Run Teleop node

    rosrun teleop_twist_keyboard teleop_twist_keyboard.py


(Optional) To re-create the PGM map
From the catkin_ws, run the following in separate terminals:

    Terminal 1:
    roslaunch pgm_map_creator request_publisher.launch
    
    Terminal 2:
    gzserver src/pgm_map_creator/world/new_world.world
