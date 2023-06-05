# Thesis_Bsc_2023_TransportationSystem
Repository for Bsc thesis of Science and Technology, a payload transportation system of a Learning Factory. 

## Requirements:
For a direct copy of the achieved system it is necessary to have:
+ Any LiDAR model 
+ Mobile robot (Although this work was validated using the Robotont, it is be possible to adapt to another mobile robot)
+ DepthCamera


Aside from hardware requirements you should also have:
ROS Noetic (if used in a new disto, some dependencies may not be available)
Ubuntu 20.04
Robotont Demo packages (see this useful guide)[https://robotont.github.io/html/files/demo_robot.html]

### For Robotont

To implement this in your own environment, it is necessary to create a map first. 
+ How to map the environment?  

  On On-board computer:
  roslaunch robotont_demos 2d_slam.launch
  roslaunch robotont_demos teleop_keyboard.launch
  On PC:
  roslaunch robotont_demos 2d_slam_display.launch
  
  After mapping the entire area save it by running 
  `rosrun map_server map_saver -f your_map_name`

* NB! If you are using a DepthCamera, remember to convert to LaserScan ()[http://wiki.ros.org/depthimage_to_laserscan]

+ How to set goal location?
After having a map, you can set the goal and base positions relative to the map.

To do that, open RViz to visualize the map. Then, in a new terminal:
`rostopic echo /robot_namespace/initialpose`

Then use the 2D Pose button to roughly select the goal and base location and pose for the robot.
You can use the values in the terminal to set both location in the code.
  
+ What about AR Tags?
Simply print them (found here)[http://wiki.ros.org/ar_track_alvar] and arrange them in a way that they lead towards the goal pose.
*i.e 0 at base and higher towards the goal*

### You can now run the code! 

*On On-board computer
To do so, simply run:
roslaunch robotont_thesis_pkg launch_sys.launch 

or, if you want to run both separately:
roslaunch robotont_thesis_pkg ar_detection.launch
roslaunch robotont_thesis_pkg main_navigation.launch

*On PC

Visualize the robot's trajectory and plan
roslaunch robotont_thesis_pkg monitoring.launch 

*NB! Keep in mind you should add the namespace of your robot after .launch if you are running the nodes separetely as well as in the monitoring node.*
