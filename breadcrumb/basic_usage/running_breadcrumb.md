---
layout: default
title:  "Running Breadcrumb"
permalink: running_breadcrumb
---

#### &uarr;[top](https://ubiquityrobotics.github.io/breadcrumb_learn/)

# Running Breadcrumb

Before the Breadcrumb starts moving it is necessary to place the markers in the desired location.
[See how to place markers](marker_info/marker_types_and_placing_them.md).

By default Breadcrumb starts in **general_mode** with touchscreen ON.
From initial pose, it will wait for the user to press START and the move to towards the detected marker.
It is important that the robot sees the first marker, otherwise it will not move.
**Touchscreen is ready once the START button and BATTERY-BARS(top-right corner) are seen.**

### Basic Breadcrumb Usage

The very basic Breadcrumb usability is to place a robot, such that it detects the first marker and it will start to move.
Breadcrumb will smoothly navigate between markers, where each marker arrow should point in the direction of the next marker.
If the robot encounters a STOP marker, it will stop on it and turn in the direction of arrow.
In case where no touchscreen is used, robot will continue it's path only if it sees a next marker in the direction it turned, otherwise it has finished its task.

To run, type:

  `roslaunch ground_fiducials ground_fiducials.launch`

or in Gazebo:

  `roslaunch ground_fiducials sim_ground_fiducials.launch`

`ground_fiducials` is our main that package, that consist of launch files that run:
- `raspicam_node` that runs onboard Raspberry Pi Camera
- `breadcrumb_description` that spawns a urdf breadcrumb model
- `pi_sonar` for collision avoidance
- `aruco_detect` or `stag_node` for detecting markers and forwarding the pose of the markers
- `breadcrumb_gazebo` for detecting markers in Gazebo
- `ground_fiducials` which handles type of markers
- `phantom_planner` that keeps track of all the goals and handles preempting
- `move_smooth` for navigation maneuvers execution

For more advance usage and capabilities refere to [Breadcrumb usage with touchscreen](touchscreen/breadcrumb_usage_with_touchscreen.md).
