# Sensory Information

```{toctree}
:maxdepth: 1
:glob:
```
------

Sensory information encompasses data such as SLAM, camera imagery, calibration, IMU, and ToF. In subsequent secondary development, these interfaces can be used to acquire and invoke data.

------

## Visual Odometry（VO）
**Function Overview：** Obtain a rapid 60Hz pose.<br>
**Topic：** `perception/visual_slam/tracking/vo_pose`<br>
**Msg Type s-e：** `geometry_msgs/msg/PoseStamped`

## SLAM Odometry
**Function Overview：** Odometry that integrates IMU and has undergone pose optimization.<br>
**Topic：** `perception/visual_slam/tracking/Odometry`<br>
**Msg Type s-e：** `nav_msgs/msg/Odometry`

## Pose Reset
**Function Overview：** Reset the odometry to zero.<br>
**Topic：** `perception/visual_slam/reset`<br>
**Msg Type s-e：** `visual_slam/reset`<br>
**Code Example：** `ros2 service call /visual_slam/reset tita_perception_msgs/srv/Reset`

## Camera Sensor Data
**Function Overview：** Publish undistorted color images from the camera at 60Hz.<br>
**Topic：**<br>
`perception/sensor/camera/left`<br>
`perception/sensor/camera/right`<br>
**Msg Type s-e：** `sensor_msgs/msg/Image`

## Camera Calibration Data
**Function Overview：** Publish camera calibration data at a frequency of 60Hz.<br>
**Topic：**<br>
`perception/sensor/camera_info/left`<br>
`perception/sensor/camera_info/right`<br>
**Msg Type s-e：** `sensor_msgs/msg/CameraInfo`

## Camera Point Cloud Data
**Function Overview：** Camera-estimated depth data, colored point cloud. Contains < 140,544 points, Point cloud distance ≤ 5 meters.<br>
**Topic：** `perception/sensor/camera/point_cloud`<br>
**Msg Type s-e：** `sensor_msgs/msg/PointCloud2`

## Camera IMU Data
**Function Overview：** Camera IMU data includes acceleration, angular velocity, and posture.<br>
**Topic：** `perception/sensor/camera/imu`<br>
**Msg Type s-e：** `sensor_msgs/msg/Imu`

## Front Face ToF Data
**Function Overview：** Front-facing ToF (Time-of-Flight) converted point cloud data. 8x8.<br>
**Topic：** `perception/sensor/spad/face/point`<br>
**Msg Type s-e：** `sensor_msgs/msg/PointCloud2`

## Lower ToF Data
**Function Overview：** Lower ToF converted point cloud data. 8x8.<br>
**Topic：** `perception/sensor/spad/neck/point`<br>
**Msg Type s-e：** `sensor_msgs/msg/PointCloud2`

## Robot Joint Coordinate System
**Function Overview：** Synchronize joint coordinates.<br>
**Topic：** `perception/wheel/tracking/odometry`<br>
**Msg Type s-e：** `tf2_msgs/msg/TFMessage`

## Wheeled Odometry
**Function Overview：** Short-range odometry. Unable to record Z-axis information.<br>
**Topic：** `perception/wheel/tracking/odometry`<br>
**Msg Type s-e：**`nav_msgs/msg/Odometry`

## Slope Detection
**Function Overview：** Based on the area that is 50 cm to one meter ahead and as wide as the robot.<br>
**Topic：**`perception/sensor/camera/attention_region`<br>
**Msg Type s-e：**`sensor_msgs/msg/PointCloud2`

## ToF-based Staircase Detection and Identification Point Cloud
**Function Overview：** Each set of four points represents a step. There are a total of eight points.<br>
**Topic：**`perception/spad/stair/point_cloud`<br>
**Msg Type s-e：**`sensor_msgs/msg/PointCloud2`

## Step Distance Recognition
**Function Overview：** The distance from the steps to the robot's base_link is calculated based on the recognized points.<br>
**Topic：**`perception/spad/stair/distance`<br>
**Msg Type s-e：**`std_msgs/msg/Float`

## Slope Angle Detection
**Function Overview：** Angle feedback of the slope detection area.<br>
**Topic：**`perception/sensor/camera/attention_region/angle`<br>
**Msg Type s-e：**`std_msgs/msg/Float`