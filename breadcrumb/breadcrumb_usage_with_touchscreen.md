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
- reboot/poweroff/reboot-software buttons
- recording ros topics to a bag file
- a screen to show the camera and joystick for debug purposes

### Breadcrumb Usage with Touchscreen

To the basic Breadcrumb usability, touchscreen UI adds an additional three features:
- In order for the Breadcrumb to start moving, start button on a touchscreen should be pressed
- During the drive, robot can be stopped by pressing the STOP button (START should be pressed to continue)
- Breadcrumb will stop on STOP marker and wait for user to press CONTINUE


### Touchscreen App main view

<img src="breadcrumb/assets/Touchscreen_main_view.png" >


The main goal for our Touchscreen App is to be as easy to use as possible.
That's why the main view is very minimalistic with one main ***START/STOP button***.
And there is also a ***CONTINUE button*** which shows up when the Breadcrumb is waiting on a STOP Marker.
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
More info about battery handling and charging can be found [here](battery.md).

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

#### Route Management option:

Breadcrumb can prioritize some markers over the others. This is particulary useful if Breadcrumb detects two or more markers at the same time (crossroad), according to the route it knows which to follow. 
For example if you have two crossroads, you should first input a marker (to the route) breadcrumb should follow in the first crossroad and then as a next marker add the one it should follow in the second crossroad.
