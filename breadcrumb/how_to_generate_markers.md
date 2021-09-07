---
layout: default
title:  "Generating Fiducials"
permalink: generating_fiducials
---

#### &uarr;[top](https://ubiquityrobotics.github.io/breadcrumb_learn/)

# Generating Fiducials

For more information about fiducial markers refer to [marker_info](marker_types_and_placing_them.md)

Scripts offer a simple UI, which enables user to re-configure fiducials according to their need.

Location of scripts is in Breadcrumb repository in the `breadcrumb/breadcrumb_detect/scripts` directory:

- `ArUco/gen_markers.py` -> generate Aruco markers with frames
- `STag/gen_markers_autogen.py` -> generate STag markers with frames by generating also the inner part.
- `STag/gen_markers.py`  -> generate STag markers with frames by getting the inner part from downloaded image library. Download the required images from [here](https://drive.google.com/drive/folders/0ByNTNYCAhWbIV1RqdU9vRnd2Vnc).

Script were tested using python2.7.

## ArUco Dictionary ID

You can generate ArUco markers from any dictionary you prefer.
Make sure you set the corresponding `dictionary` parameter in launch file.
We performed most of the test with dictionary with **ID 7**.
For more information about ArUco refer to [`ArUco`](http://docs.opencv.org/trunk/d5/dae/tutorial_aruco_detection.html).

## STag Library HD

You can generate STag markers from any library you prefer.
Make sure you set the corresponding `libraryHD` parameter in launch file.
We performed most of the test with library **HD15**, which suited our needs.
For more infomation about STag refer to [`STag`](https://github.com/usrl-uofsc/stag_ros).

## Packs

Generally each pack should correspond to a standalone route, but you can generate yourself packs according to your preference.
Take note that each marker has a unique id, while a number is unique only to the pack.
