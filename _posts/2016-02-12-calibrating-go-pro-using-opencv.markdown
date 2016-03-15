---
layout: post
title:  "Calibrating a Gopro camera using OpenCV"
date:   2016-02-12 10:28:51 +0100
categories: opencv gopro calibration
---

[OpenCV](http://opencv.org) is the most used open source library for the computer vision community. It contains hundreds of functions and utilities that save hours of programming to its users.
One of the most used modules is [Camera Calibration and 3D Reconstruction](http://docs.opencv.org/2.4/modules/calib3d/doc/camera_calibration_and_3d_reconstruction.html) that allow to calibrate cameras and undistort the output images.
Calibrating a camera is not a complicated task for normal cameras and there are many sites with extensive descriptions about how to achieve a good calibration with OpenCV, but problems start when trying to calibrate wide-angle and fisheye lenses with the standard module.

The standard module that was based on [Bouguet's Toolbox](http://www.vision.caltech.edu/bouguetj/calib_doc/) was not thought to calibrate wide-angle and fisheye lenses but rectilinear cameras.

Surfing the net, one can found multiple forum entries and questions about people trying to calibrate a GoPro camera with the standard module that most likely leads to undesired results or problems.
With lots of pacience and the appropiate number of parameters it is possible to achieve an acceptable result.

For example, calibrating a GoPro Hero 4 Black camera in 12Mpx Image mode with 4 radial distortion parameters, gives the following results:

![alt text](/post_images/GOPR0283.JPG  "Original Image" )

![alt text](/post_images/GOPR0283_rect_0.JPG "Undistorted image (Alpha 0)")

With an RMS of 1.3 px, that given the distortion of the original images seems reasonable. Everything looks great until here. The surprise comes when people tries to "zoom out" the image in order to see all the information that was in the original one, and not the cropped version.

![alt text](/post_images/GOPR0283_rect.JPG "Undistorted image (Alpha 1)")

Looking at the picture above we can clearly see that the corners of the image are highly distorted. Vertical lines look curvy making this regions of the image unusable for any application.

Fortunately, since OpenCV 2.4.10 comes with a set of functions especially designed for fisheye lenses that can deal with heavy distortions like the GoPro images.

![alt text](/post_images/GOPR0283_rect_fish.JPG "Undistorted image (Fisheye Model)")


{% highlight python %}

#!/usr/bin/env python

import numpy as np
import cv2
import glob
import os
import tarfile 
import ipdb
import math
from matplotlib import pyplot as plt

image_w=1616
image_h=1232

def cal_from_tarfile(tarname, size, calib_flags = 0, visualize = False, alpha=1.0, delay=5):

{% endhighlight %}
