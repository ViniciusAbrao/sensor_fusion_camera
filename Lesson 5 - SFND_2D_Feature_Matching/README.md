# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

## RUBRIC POINTS

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load:

In the file MidTermProject_Camera_Student.cpp, lines 75-78, the ring buffer is implemented. 

* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed:

In the file matching2D_Student.cpp, the functions detKeypointsShiTomasi(), detKeypointsModern() and detKeypointsHarris() are used to implement the keypoint detectors.
In the file MidTermProject_Camera_Student.cpp, lines 112-118, only keypoints on the preceding vehicle are selected.

* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson:

In the file matching2D_Student.cpp, lines 57-92, the descriptor extractors are implemented.
In the file matching2D_Student.cpp, lines 21-26 and 37-48, the FLANN aproach and the k nearest neighbors with filter matches using descriptor distance ratio test, are respectively implemented.

* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures:

In the file MidTermProject_Camera_Student.cpp, lines 46-51, the detector and descriptor types are selected in order to compare the performances measures.

## TOP 3 combinations found

1. FAST detector. ORB descriptor.
2. FAST detector. BRISK descriptor.
3. ORB detector. BRISK descriptor.

## MP.9 Performance Evaluation 3

See the results in the file results.pdf



