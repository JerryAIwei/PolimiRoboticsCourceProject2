Team member:
Shaoxun Xu 10730116
Aiwei Yin 10730328
Jiaying Lyu 10735282

# Description of the files inside the archive:

|--ekf
|  |--ekf.launch #configuration of the ekf
|-- gmapping
|  |--gmapping.launch #configuration of the gmapping
|--map
|  |--map_optitrack.pgm #map created by optitrack odometry
|  |--map_optitrack.yaml
|  |--map_visual.pgm #map created by visual odometry, used for move_base
|  |--map_visual.yaml
|--move_bases
|  |--amcl.launch #configuration of the amcl
|--point2laser
|  |--pointcloud_to_laser.launch #convert pointcloud to laser scan
|--tf
|  |--static_tf_optitrack.launch #static tf for optitrack odometry
|  |--static_tf_visual.launch #static tf for visual odometry
|--gmapping_optitrack.launch #start everything for creating map via optitrack odometry
|--ekf
|  |--ekf.launch #ekf for fuse imu and visual odometry
|  |--ekf_template.yaml #parameters for ekf
|  |--imu_filter.launch #get orientation from the raw imu data
|--gmapping_visual.launch #start everything for creating map via visual odometry
|--gmapping_imu.launch #start everything for creating map via IMU fused visual odometry
|--move_based_amcl.launch #localization of the robot in a given map via lidar and visual odometry
|--move_based_amcl_imu.launch #localization of the robot in a given map via lidar and IMU fused visual odometry

# Structure of the tf tree:
see the images in tf_graph
     

Build map: 2020-05-14-16-09-36-traj1-os1-t265-pix.bag
Test move_base: 2020-05-14-16-14-37-traj2-os1-t265-pix.bag


# usage:

We test our project on ubuntu 18.04 with ROS Melodic

Prerequisites:

install gmapping, amcl, pointcloud-to-laserscan and robot-pose-ekf

Running:

cd to 10730328

build map via optitrack odometry

```
roslaunch gmapping_optitrack.launch
```
run the bag in another terminal with clock
```
rosbag play --clock 2020-05-14-16-09-36-traj1-os1-t265-pix.bag
```
when the bag finish, use map server to save the map 
 
-------------------------------------------------------
build map via visual odometry

```
roslaunch gmapping_visual.launch
```
run the bag in another terminal with clock
```
rosbag play --clock 2020-05-14-16-09-36-traj1-os1-t265-pix.bag
```
when the bag finish, use map server to save the map

--------------------------------------------------------
build map via imu and visual odometry

```
roslaunch gmapping_imu.launch
```
run the bag in another terminal with clock
```
rosbag play --clock 2020-05-14-16-09-36-traj1-os1-t265-pix.bag
```
when the bag finish, use map server to save the map

--------------------------------------------------------
test move_base

put the map made by visual odometry and the .yaml file into map folder
The names should be map.pgm and map.yaml

run amcl
```
roslaunch move_base_amcl.launch
```
run the bag in another terminal with clock
```
rosbag play --clock 2020-05-14-16-14-37-traj2-os1-t265-pix.bag
```
--------------------------------------------------------
test move_base

put the map made by visual odometry and the .yaml file into map folder
The names should be map.pgm and map.yaml

run amcl
```
roslaunch move_base_amcl_imu.launch
```
run the bag in another terminal with clock
```
rosbag play --clock 2020-05-14-16-14-37-traj2-os1-t265-pix.bag
```

# Info you think are important/interesting:

The most important part of the project is to undersand the tf relationship of each frame. Meanwhile, the visualization tools in ROS, like rviz, rqt_tf, rqt_topic are very helpful for debugging. 

The IMU data is really noise, it seems it would not improve the visual odometry.





