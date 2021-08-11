---
layout: default
title:  "Running Breadcrumb"
permalink: running_breadcrumb
---

#### &uarr;[top](https://ubiquityrobotics.github.io/breadcrumb_learn/)

# Running Breadcrumb

Before the Breadcrumb starts moving it is necessary to place the markers in the desired location.
[See how to place markers](marker_info/marker_types_and_placing_them.md).

**Touchscreen is ready once the START button and BATTERY-BARS(top-right corner) are seen.**
Innitialy when robot is boot up, touchscreen display shows an Innitializing screen. After the system is ready you should be able to see a screen with a START button.
From initial pose, it will wait for the user to press START and the move to towards the detected marker.
It is important that the robot sees the first marker, otherwise it will not move.

### Basic Breadcrumb Usage

The very basic Breadcrumb usability is to place a robot, such that it detects the first marker and it will start to move.
Breadcrumb will smoothly navigate between markers, where each marker arrow should point in the direction of the next marker.
If the robot encounters a STOP marker, it will stop on it and turn in the direction of arrow.
In case where no touchscreen is used, robot will continue it's path only if it sees a next marker in the direction it turned, otherwise it has finished its task.

To run, type:

  `roslaunch ground_fiducials ground_fiducials.launch`

or in Gazebo:

  `roslaunch ground_fiducials sim_ground_fiducials.launch`

`ground_fiducials` is our main package, that consist of launch files running:
- `raspicam_node` that starts onboard Raspberry Pi Camera
- `breadcrumb_description` that spawns a urdf breadcrumb model
- `pi_sonar` for collision avoidance
- `breadcrumb_detect` for detecting markers and forwarding the pose of the markers
- `ground_fiducials` which handles type of markers
- `breadcrumb_nav` which handles navigation maneuvers execution

For more advance usage and capabilities refere to [Breadcrumb usage with touchscreen](../touchscreen/breadcrumb_usage_with_touchscreen.md).
