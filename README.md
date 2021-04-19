# Scan Matching Localization

Self-Driving Car Engineer Nanodegree<br/>
https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013

# Installation

Go to the Udacity workspace of the project "Scan Matching Localization" of the Lesson 3 "Localization" of the Self-Driving Car Engineer Nanodegree.

Copy the contents of the file [c3-main.cpp](c3-main.cpp) into the file `/home/workspace/c3-project/c3-main.cpp` in the Udacity workspace of the project "Scan Matching Localization". You can do it by copying and pasting the contents of the file [c3-main.cpp](c3-main.cpp).

# Usage

Enable GPU Mode. Press the blue button "Desktop". Start one terminal in Desktop. Run the Carla simulator by using these Unix commands:

```
su - student # Ignore Permission Denied, if you see student@ you are good
cd /home/workspace/c3-project
./run_carla.sh
```

Start another terminal in Desktop. Compile the project by using these Unix commands:

```
cd /home/workspace/c3-project
cmake .
make
```

Run the project with the NDT algorithm by using Unix command:

```
./cloud_loc
```

Or run the project with the ICP algorithm by using Unix command:

```
./cloud_loc 2
```

Once the project is running, click on the map and tap the UP key 3 times. This improved version of the project normally works at the first run. However, if the green car gets left behind, run the project again and tap the UP key 3 times again.

The NDT algorithm works better than the ICP algorithm. Even if the car hits the wall at the end, the NDT algorithm will not produce an error greater than 1.2 meters.

# Algorithm Upgrade

This version of the project works better than my first submission because I stored the 6 last estimated X coordinates of the car in order to compute the estimated average speed of the car in the X axis. Then, I added the average speed to the X coordinate of the initial guess. When I read the paper "Robust localization using 3D NDT scan matching with experimentally determined uncertainty and road marker matching" <https://www.researchgate.net/publication/318801657_Robust_localization_using_3D_NDT_scan_matching_with_experimentally_determined_uncertainty_and_road_marker_matching>, I noticed that the researchers use a grid of many initial guesses to improve the fitness score of the NDT algorithm. Given the linear unidirectional nature of the car trajectory of this project, I think it was enough to use only 1 initial guess: The estimated pose plus the average speed of the X coordinate.

Moreover, the instructor also suggested to decrease the number of maximum iterations. And I decrease the number of maximum iterations from 60 to 4. This change produced a fitness score similar to the previous version and a process time 10 times faster than the previous version.


# Video Demonstrations

For this second submission, I captured the video directly from the Udacity workspace; and the play speed of the video is the same speed in which the video was recorded. I didn't speed up the video like I did in my first submission.

**Scan Matching Localization with LIDAR Point Clouds - NDT Algorithm (Improved)<br/>
https://youtu.be/Im1PoP6d7y0**
![NDT_Passed.png](/images/NDT_Passed.png)

**Scan Matching Localization with LIDAR Point Clouds - ICP Algorithm (Improved)<br/>
https://youtu.be/2NkOorRFwPA**
![ICP_Passed.png](/images/ICP_Passed.png)
