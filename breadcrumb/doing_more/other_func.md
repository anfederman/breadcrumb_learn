---
layout: default
title:  "Other features of Magni robot"
permalink: other_func
---

#### &uarr;[top](https://ubiquityrobotics.github.io/breadcrumb_learn/)

- Breadcrumb can be connected with your workstation, which can be so that graphical tools such as RViz or plotting software can be run on the screen and many other features. For more informationrefer to [Connecting a Workstation and Starting the Robot](https://learn.ubiquityrobotics.com/connecting).
- Everytime system is running it is populating logs, which eventually becomes full. Cleaning log files can be done manually or with the help of our scripts which deletes logs automatically after a predefined number of days, you set for yourself in the script found [here](https://github.com/UbiquityRobotics/breadcrumb/blob/finalization/breadcrumb_bringup/scripts/ros_log_clean.bash).
- Beside driving the robot you can also dynamically modify parameters using dynamic_reconfigure. To run, type:

        rosrun rqt_reconfigure rqt_reconfigure

Each nodes that offers to be configured will be listed in the window this command will open.
