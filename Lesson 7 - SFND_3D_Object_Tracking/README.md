# SFND 3D Object Tracking

Welcome to the final project of the camera course. Let's take a look at our program schematic to see what we already have accomplished and what's still missing.

<img src="images/course_code_structure.png" width="779" height="414" />

In this final project, I have implemented the missing parts in the schematic. To do this, I follow four major tasks: 

1. First, I developed a way to match 3D objects over time by using keypoint correspondences:

 In the file camFusion_Student.cpp, lines 267-306, I implemented the function matchBoundingBoxes() to obtain the match list of 3D objects between current and previous frame. 
 
2. Second, I computed the TTC based on Lidar measurements. 

In the file camFusion_Student.cpp, lines 227-264, I implemented the function computeTTCLidar() to compute TTC based on the Lidar data.

3. I proceed with the same using the camera. It requires to first associate keypoint matches to regions of interest and then to compute the TTC based on those matches:

The first part is done in the file camFusion_Student.cpp, lines 142-168, where I implemented the function clusterKptMatchesWithROI().

In the file camFusion_Student.cpp, lines 172-224, I implemented the function computeTTCCamera() to compute TTC based on the Camera data.

4. And lastly, I conduct various tests with the framework. Your goal is to identify the most suitable detector/descriptor combination for TTC estimation and also to search for problems that can lead to faulty measurements by the camera or Lidar sensor. 

In the file FinalProject_Camera.cpp, lines 77 and 80, the detector and descriptor types are selected in order to compare the performances measures. The results are shown for the top 3 combinations found in the mid term project:

i. FAST detector. ORB descriptor.
ii. FAST detector. BRISK descriptor.
iii. ORB detector. BRISK descriptor.

The TTC results are shown in the file results.pdf.

## Performance Evaluation 

It is observed that outliers may lead to false results. The solution implemented to reduce that influence is based on to compute the median distance instead of min distance in the TTC based on the Lidar data. The similar is done in TTC based on the Camera data, in which the mean distance ratio is considered.

In the case of Camera based TTC, different combination of detector/descriptor may lead to erroneous results, that are observed in the FAST/BRISK and ORB/BRISK combinations. The reason is probably because of incluence of the wrong key points matches, that lead to wrong values of median distance ratio and TTC.

In the FAST/ORB combination, the results shown similar values from both TTC based on the Lidar and Camera, that enable the algorithm validation.

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level project directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./3D_object_tracking`.
