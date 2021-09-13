---
layout: default
title:  "Visualize with RViz"
permalink: rviz
---

#### &uarr;[top](https://ubiquityrobotics.github.io/breadcrumb_learn/)

# Visualize with RViz

Rviz (ROS visualization) is a 3D visualizer for displaying sensor data and state information from ROS. It can show the robot in space as well as graph practically any robot parameter.

There is a nice short introductory rviz video at [this location](http://wiki.ros.org/rviz).

To run, type

  ```roslaunch breadcrumb_demos demo_world.launch```

![rviz](https://ubiquityrobotics.github.io/breadcrumb_learn/breadcrumb/assets/rviz_image.png)

Using rviz, you can move the robot:
Click on "2D Nav Goal" in the menu bar.
Click again in the black screen area and indicate what the robot is to do.

Here is a [short video](https://ubiquityrobotics.github.io/breadcrumb_learn/breadcrumb/assets/rviz_with_nav.mp4) showing the robot navigating with our setup.

In the right hand window you see the steps that are carried out on the workstation including loading rviz etc.

Once RViz is loaded you can see that the user issues a go to goal target in RViz using a few mouse clicks. She first clicks **2D Nav Goal** in the menu bar, then clicks on the desired pose. The arrow that is on the field of view is the desired location and orientation.
