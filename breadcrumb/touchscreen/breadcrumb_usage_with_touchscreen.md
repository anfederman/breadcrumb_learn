---
layout: default
title:  "Breadcrumb usage with Touchscreen UI"
permalink: breadcrumb_usage_with_touchscreen
---

#### &uarr;[top](https://ubiquityrobotics.github.io/breadcrumb_learn/)

# Touchscreen UI

Web application made for the 7'' touchscreen monitor for Raspberry Pi.
The main functionality is to manage routes for Breadcrumb.
It includes:
- start/stop button to start/stop the robot
- a continue button for robot to continue after stopping on stop marker
- settings - UI for the routes management
- reboot/poweroff buttons
- recording ros topics to a bag file
- a screen to show the camera for debug purposes

### Breadcrumb Usage with Touchscreen

To the basic Breadcrumb usability, touchscreen UI adds an additional three features:
- In order for the Breadcrumb to start moving, start button on a touchscreen should be pressed
- During the drive, robot can be stopped by pressing the STOP button (to continue, start should be pressed)
- Breadcrumb will stop on Stop marker and wait for user to press continue


### Touchscreen app main view

<img src="breadcrumb/assets/Touchscreen_main_view.png" >


The main goal for our Touchscreen Application is to be as easy to use as possible.
That's why the main view is very minimalistic with one main ***START/STOP button***.
And there is also a ***CONTINUE button*** which shows up when the Breadcrumb is waiting on a Stop Marker.
On top of the screen you can see buttons (from left to right):

- Display camera view
- Reboot and power off
- Exit to desktop
- Record ROS topics to rosbag

The battery status is located on the top right side.
Battery low warning shows as a Pop-Up View  when the battery gets lower than 40%.
Settings button is located below the battery icon.
It is used mostly for Route management which is described below.

### Route management

The very basic Breadcrumb usability is very limited.
The route management functionality allows Breadcrumb robot to navigate itself in a more advanced level.
If you press the settings button on the touchscreen UI you'll see the main route management page.
There you can create, edit, delete new routes.
The route represents the instructions for the Breadcrumb on how to follow the markers.
There is also a list of ignored markers.
When you press the desired route it turns green in the settings page, and when the start is pressed the robot will search for the 1. marker on the route list.
When it moves to that marker it starts to look after the 2. one and so forth till the last one.
On the last one the Breadcrumb starts searching for the 1. one and basically this loop can last forever :)
or till the batteries are empty.
More info about battery handling and charging can be found [here](../battery.md).

<br>
Route management view can be found by pressing the Settings button on the main view.
<img src="breadcrumb/assets/Touchscreen_settings.png" >
The left column shows list of all your routes.
You can add new one by pressing + button.
One of the routes is colored green and that is your current route that robot will follow.
If you press the pencil on a desired route, the Set up Route view shows up on right side of the screen.
There you can edit or delete that route.
The left column of Set up Route (which is on a center of the screen) shows main instructions for Breadcrumb.
When the START is pressed, the Breadcrumb starts looking for the 1. Marker on that list and continues till the last one.
The Don't Follow list of markers is on the right of the screen.
The Breadcrumb will always ignore all the Markers on that list so you should be careful on which Marker you really want to ignore all the time.

The Marker on both columns can be easily moved to another position by drag and drop technique.
But sometimes the list becomes too big for the screen so there is a lock button to lock the drag and drop and after that you can scroll each column without changing the Marker sequence by mistake.

#### Route Management modes:

Route modes: the route can be followed very strictly or more like a recommended mode, e.g.
- **Strict mode:** the Breadcrumb moves only towards the next marker that is specified in the selected route, and it ignores all the rest.

        roslaunch ground_fiducials ground_fiducials.launch touchscreen:=true mode:=strict_mode

- **Turn mode:** the Breadcrumb ignores all TURN markers if not set as a priority in a route list.
    	The idea here is to modify the route list faster and with less marker insertions, while following a set of rules:
		- TURN markers should be positoned only on the crossroads.
		- Since most of the TURN markers will be ignored, make sure that each crossroad should either have a TURN marker specified in a chosen route or GO, BIDIRECTIONAL or STOP marker.

	roslaunch ground_fiducials ground_fiducials.launch touchscreen:=true mode:=turn_mode

- **General mode:**
    There are no crossroads, only a standalone positioned markers representing a route from START (GO Marker) to the STOP(STOP marker).
    When it sees a marker it sends goal to move there. This mode offers a one-way route.

        roslaunch ground_fiducials ground_fiducials.launch touchscreen:=true mode:=general_mode

Ignoring markers: Touchscreen enables user to ignore certain markers.
    This is useful, if no one of the modes suits your need. The list of ignored markers can be set in settings.

Depending on which markers you choose, you should run launch file correspondingly. e.g. to use with ArUco:

        roslaunch ground_fiducials ground_fiducials.launch aruco:=true stag:=false

Breadcrumb by default starts in **general_mode** with **Touchscreen enabled**.
