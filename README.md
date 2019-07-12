# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load. 
* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed. 
* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson. 
* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures. 

See the classroom instruction and code comments for more details on each of these parts. Once you are finished with this project, the keypoint matching part will be set up and you can proceed to the next lesson, where the focus is on integrating Lidar points and on object detection using deep-learning. 

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.

## MP1

To implement the dataBuffer we keep the track in size of the buffer and every time the size of the buffer exceed the max we remove the last image from the Buffer.

## MP2 

We modified the file matching2D.cpp to implement HARRIS, FAST, BRISK, ORB AKAZE and SIFT detectors. 


After some test with all detectors, we could notice the FAST detector result the more numbers of keypoints. AKAZE and BRISK resulted in a good amount of keypoints too.


## MP3

The number of keypoints was limited by a rectangle, where should be located the vehicle in front of the car. We used the opencv's cv::Rect and cv::Rect::contains

## MP4

We implemented the BRIEF, ORB, FREAK, AKAZE and SIFT descriptors and we make they selectable by a setting string.

## MP5 

FLANN matching and KNN selection was implement. 

OBS. In the current OpenCV  version (4.0.1) there is a bug in the FLANN implementation.Bug workaround : convert binary descriptors to floating point 

## MP6

We implement a KNN matchim, which look at the ratio of the best and second-best match to decide whether to keep an assoated pair of keypoints

## MP7 & MP8 & MP9

We have compared all detectors and descriptor, please see the xlsx file in this repo

### TOP 3

1. FAST detector / ORB describer 
2. FAST detector / BRIEF describer

This TOP 2 was chose based in the velocity, the FAST detector was the fastest in all cases. And it was able to detect in 1.5 m/s
,with the ORB describer was able to match with keypoint with 0.009 m/s and a success rate of 25.77%
 
3. SIFT detector / FREAK describer

This on was the slowest case, but in other hand, it was 52.74% of matches. If the velocity of the process it's not so important this should be your choice.
