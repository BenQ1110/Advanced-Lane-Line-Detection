# Advanced Lane Lines Detection 

## Overview

This project is part of my Self-Driving course at Udacity. It identifies the lane boundaries in a video and shows information like distance of centre and radius of curvature.

## Code

1. Camera Calibration

All the calibration images (chess board images) are loaded using glob.glob. Each frame is converted to grayscale. The chessboard corners are identified and those points are added to imgpoints. Objp is an array of coordinates, and objpoints stores its copy every time chessboard is detected. To check the results, a chessboard with corners is displayed using cv2.drawChessboard Corners. Subsequently, camera matrix and distortion coefficients are acquired using cv2.calibrateCamera(). At the end, distortion correction is used on the test image (cv2.undistort()). 

2. Pipeline

a) The image is distortion-corrected.
b) Binary image is created.

I use only colour thresholds as they provide enough information to identify the lines. First, I limit the area to the area in front of the vehicle using the region_of_interest function. Subsequently, I use colour thresholds using the color_th function. RGB and HLS colour spaces were used. Red and green enabled to identify bright yellow lines and white lines, whereas hue and lightness were used to identify darker yellow parts.

c) Perspective Transoform is applied

I identify the source points and destination points.  Subsequently, the warped image is acquired using the cv2.getPerspectiveTranform and cv2.warpPerspective functions. 

d) Lane Line Pixels 

A histogram of a binary image is created. Then the method called sliding windows is employed. The starting points are identified using np.argmax (leftx_base, rightx_base). The number of windows implemented is 40 but a smaller number would be sufficient. Then each window with non-zero pixels is identified one by one. Indices of the appropriate box are added to the list. Subsequently, new windows is created on previous window’s mean position. When the process is finished, second order polynomial is fitted to a left and right indices using np.polyfit. Then x and y values required for plotting were identified. 

## Output
The output of the pipeline is uploaded as well. 

## Comments 

I think that the model performs well with yellow and white lines taking into consideration shadows and changes in the colour of the road. However, employment of the gradient thresholds would make the model more robust in case the shade of the lines doesn’t match colour thresholds. Moreover, it would be advisable to use some averaging function between the lines, so they appear smoother and hence are safer for the vehicle. 
