---
layout: default
title:  "Modifying navigation parameters"
permalink: tuning_nav
---

#### &uarr;[top](https://ubiquityrobotics.github.io/breadcrumb_learn/)

# Breadcrumb Navigation Stack

`breadcrumb_nav` is the main ROS package that consist of:
- **Planning of the goals** (Phantom planner)
- **Execution of navigation goals** (Move Smooth)
- **Collision avoidance** based on LiDAR and/or Sonars

## Node Details 

You can skip that part if you are not interested in the internals.

### Phantom planner

Phantom planner node handles planning of navigation goals, sending them forward to `move_smooth`. 
We are using `phantom_planner` node to plan two different types of goal: **Fiducial goal** and **Phantom goal**. 
- **Fiducial goal** is in the origin of the Fiducial marker coordinate frame, whose state can be transformed using tf into any other tf frame (e.g. base_link)
- **Phantom goal** is just like any goal, only that its purpose is to serve as a next goal(second goal in the Action Server queue), which enables
the robot to make a smooth transition from following the first goal to the phantom goal. e.g. In case there wouldn't be any next goal robot would stop at first.

Correspondingly there are two ROS Services:
- `send_fiducial` handles sending/preempting Fiducial goal
- `send_phantom` handles sending/preempting Phantom goal

In practical terms, the two goals are equal, our idea was to distinguish the two since the both serve for a different purpose.
In case of Breadcrumb, the purpose of phantom goal is for the robot to blindly drive in the direction in
which marker points (planning in Fiducial frame), until it detects a new marker. When it detects a new marker it preempts the
phantom goal and removes it from the Queue on the Action Server and sends a pair of Fiducial goal and a new Phantom goal 
according to this new detected marker.

### Move Smooth

Move smooth is a navigation node that receives a maximum of two goals at a time in an arbitrary frame and executes navigation maneuvers to arrive to the goals.
If more than two goals are send, the QueuedActionServer(Custom ROS Action Server running in parallel to move_smooth) preempts the first goal send, starts executing the next(second) goal in the queue and adds the new goal to the queue. 

### Collision Avoidance

If data from a laser scanner or sonars is available, collision avoidance can be performed. If an obstacle is detected, it will slow or stop in an attempt to avoid a collision.

## Dynamically Reconfigure Navigation parameters

While Breadcrumb is running, you can modify its velocity or change the stopping distance of the robot in order to prevent collision etc.
Before proceeding you should make sure Breadcrumb is connected to the network (https://learn.ubiquityrobotics.com/connect_network) and your workstation synced with Breadcrumb (https://learn.ubiquityrobotics.com/workstation_setup). 
In order to do so, open a terminal on your workstation and run:

    rosrun rqt_reconfigure rqt_reconfigure
    
This will open up a UI where on the left side you choose `move_smooth`. 
Then you can choose to modify multiple parameters:

* **`max_angular_velocity`** (double, default: 1.0, min: 0, max: 4.0)

	Maximum turning velocity on spot.

* **`min_angular_velocity`** (double, default: 0.2, min: 0, max: 4.0)

  Minimum turning velocity on spot.
  
* **`max_angular_acceleration`** (double, default: 0.3, min: 0, max: 4.0)

	Maximum turning acceleration during on spot rotation.

* **`max_linear_velocity`** (double, default: 0.5, min: 0, max: 1.1)

	Maximum linear velocity.

* **`max_linear_acceleration`** (double, default: 0.5, min: 0, max: 1.1)

	Maximum linear acceleration.

* **`smooth_decceleration`** (double, default: 0.17, min: 0, max: 1.1)

	Decceleration to stop.

* **`max_linear_in_turn_velocity`** (double, default: 0.4, min: 0, max: 1.1)

	Maximum linear velocity during the turn.

* **`max_lateral_acceleration`** (double, default: 0.8, min: 0, max: 4.0)

	Maximum lateral acceleration during lateral correction.

* **`linear_tolerance`** (double, default: 0.1, min: 0, max: 1.0)

	Within linear tolerance, linear error is negligible.

* **`angular_tolerance`** (double, default: 0.1, min: 0, max: 1.0)

	Within angular tolerance, orientation error is negligible.
  
* **`max_incline_without_slipping`** (double, default: 0.3, min: 0, max: 5.0)

	Maximum incline of the robot turned sideways before starting to slip (Constant determined based of physical properties of the robot).
 
* **`max_lateral_deviation`** (double, default: 0.2, min: 0, max: 5.0)

	Maximum lateral deviation from the planned path.
  
* **`angle_boundary`** (double, default: 15.0, min: 0, max: 50.0)

	Angle at which we transition from turning to small lateral corrections.
  
* **`min_side_dist`** (double, default: 0.3, min: 0, max: 5.0)

	Minimum distance to maintain at each side.
  
* **`forward_obstacle_threshold`** (double, default: 0.5, min: 0, max: 3.0)

	Minimum distance to maintain in front.
