# SFND 3D Object Tracking

Welcome to the final project of the camera course. Let's take a look at our program schematic to see what we already have accomplished and what's still missing.

<img src="images/course_code_structure.png" width="779" height="414" />

In this final project, I have implemented the missing parts in the schematic. To do this, I follow four major tasks: 

1. FP.1 - First, I developed a way to match 3D objects over time by using keypoint correspondences:

 In the file camFusion_Student.cpp, lines 267-306, I implemented the function matchBoundingBoxes() to obtain the match list of 3D objects between current and previous frame. 
 
 In order to select the bouding box matches, it is tracked how many key points are in both the ith and jth bound box from previous and current frames. A 2D array is used to store the number of counts and a last nested loop for all the BB matches select that with highest occurrencies.
 
 
2. FP.2 - Second, I computed the TTC based on Lidar measurements. 

In the file camFusion_Student.cpp, lines 227-264, I implemented the function computeTTCLidar() to compute TTC based on the Lidar data.

Instead of to use the minimum distance in the X direction to the vehicles's rear, the median distance to Lidar points within ego lane is computed in each frame. That minimize the outliers influence and in the sequence the TTC can be computed with the median distance of previous (medPrev) and current (medCurr) frames, taking the equation of constant velocity model:

    TTC = medCurr * dT / (medPrev - medCurr);

3. I proceed with the same using the camera. It requires to first associate keypoint matches to regions of interest and then to compute the TTC based on those matches:

The first part (FP.3) is done in the file camFusion_Student.cpp, lines 142-168, where I implemented the function clusterKptMatchesWithROI().
The function first get the keypoint and its matched partner in the prev. frame; next compute the distances; in the sequence is computed the mean distance of keypoints in one frame with respect to their mach in the previous frame. So, it is associated a given bounding box with the keypoints it contains, however, filtering that kp which the distance is greater than the mean, since it can be a outlier.

Second, FP.4, in the file camFusion_Student.cpp, lines 172-224, I implemented the function computeTTCCamera() to compute TTC based on the Camera data.
The TTC based on the camera is obtained by first computing the distances for all keypoints between curr. and prev. frames. This is done with an outer and an inner loops. Next, using the median distance ratios to minimize the influence of outliers, the following equation of constant velocity model is used to compute the TTC:

    TTC = -dT / (1 - medDistRatio);

4. Lastly, I conduct various tests with the framework. Your goal is to identify the most suitable detector/descriptor combination for TTC estimation and also to search for problems that can lead to faulty measurements by the camera or Lidar sensor. 

In the file FinalProject_Camera.cpp, lines 77 and 80, the detector and descriptor types are selected in order to compare the performances measures. The results are shown for the top 3 combinations found in the mid term project:

i. FAST detector. ORB descriptor.
ii. FAST detector. BRISK descriptor.
iii. ORB detector. BRISK descriptor.

The TTC results and figures (FP.5) are shown in the file results.pdf. 

## Performance Evaluation - FP.6

It is observed that outliers may lead to false results. The solution implemented to reduce that influence is based on to compute the median distance instead of min distance in the TTC based on the Lidar data. The similar is done in TTC based on the Camera data, in which the mean distance ratio is considered.

In the case of Camera based TTC, different combination of detector/descriptor may lead to erroneous results, that are observed in the FAST/BRISK and ORB/BRISK combinations. The reason is probably because of incluence of the wrong key points matches, that lead to wrong values of median distance ratio and TTC.

In the FAST/ORB combination, the results shown similar values from both TTC based on the Lidar and Camera, that enable the algorithm validation.

Another reason for incorrect TTC results is the constant velocity model used. This is because when the vehicles is breaking hard, the velocity is not constant and the constant acceleration should be used instead. 

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level project directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./3D_object_tracking`.
