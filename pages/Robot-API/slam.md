# 感知信息

```{toctree}
:maxdepth: 1
:glob:
```
------

感知信息包括了SLAM、相机图像、标定、IMU、Tof等数据。在后续二次开发中可以通过以上这些接口进行数据获取和调用。

------

## 纯视觉里程计（VO）
**功能概述：** 获得快速的60hz位姿。<br>
**Topic：** `perception/visual_slam/tracking/vo_pose`<br>
**Msg Type s-e：** `geometry_msgs/msg/PoseStamped`

## SLAM里程计
**功能概述：** 融合imu且进行了位姿优化的里程计。<br>
**Topic：** `perception/visual_slam/tracking/Odometry`<br>
**Msg Type s-e：** `nav_msgs/msg/Odometry`

## 姿态重置
**功能概述：** 将里程计清零。<br>
**Topic：** `perception/visual_slam/reset`<br>
**Msg Type s-e：** `visual_slam/reset`<br>
**命令示例：** `ros2 service call /visual_slam/reset tita_perception_msgs/srv/Reset`

## 相机图像
**功能概述：** 发布相机去畸变后的彩色图像 60hz。<br>
**Topic：**<br>
`perception/sensor/camera/left`<br>
`perception/sensor/camera/right`<br>
**Msg Type s-e：** `sensor_msgs/msg/Image`

## 相机标定数据
**功能概述：** 发布相机标定数据 频率60hz。<br>
**Topic：**<br>
`perception/sensor/camera_info/left`<br>
`perception/sensor/camera_info/right`<br>
**Msg Type s-e：** `sensor_msgs/msg/CameraInfo`

## 相机点云数据
**功能概述：** 相机估计的深度数据，彩色点云。小于140544个点。点云距离小于5m。<br>
**Topic：** `perception/sensor/camera/point_cloud`<br>
**Msg Type s-e：** `sensor_msgs/msg/PointCloud2`

## 相机imu数据
**功能概述：** 相机imu加速度，角速度，姿态。<br>
**Topic：** `perception/sensor/camera/imu`<br>
**Msg Type s-e：** `sensor_msgs/msg/Imu`

## 前脸Tof数据
**功能概述：** 前脸tof转换的点云数据。8x8<br>
**Topic：** `perception/sensor/spad/face/point`<br>
**Msg Type s-e：** `sensor_msgs/msg/PointCloud2`

## 下巴Tof数据
**功能概述：** 下巴tof转换的点云数据。8x8<br>
**Topic：** `perception/sensor/spad/neck/point`<br>
**Msg Type s-e：** `sensor_msgs/msg/PointCloud2`

## 机器人关节坐标系
**功能概述：** 同步关节坐标。<br>
**Topic：** `perception/wheel/tracking/odometry`<br>
**Msg Type s-e：** `tf2_msgs/msg/TFMessage`

## 轮式里程计
**功能概述：** 短距离里程计。不可记录z信息。<br>
**Topic：** `perception/wheel/tracking/odometry`<br>
**Msg Type s-e：**`nav_msgs/msg/Odometry`

## 坡度检测
**功能概述：** 根据前方50cm到一米与机器人等宽的区域。<br>
**Topic：**`perception/sensor/camera/attention_region`<br>
**Msg Type s-e：**`sensor_msgs/msg/PointCloud2`

## Tof台阶检测识别点云
**功能概述：** 每四个点表示一个台阶。共八个点。<br>
**Topic：**`perception/spad/stair/point_cloud`<br>
**Msg Type s-e：**`sensor_msgs/msg/PointCloud2`

## 台阶距离识别
**功能概述：** 根据上述识别点计算的台阶距机器人base_link的距离。<br>
**Topic：**`perception/spad/stair/distance`<br>
**Msg Type s-e：**`std_msgs/msg/Float`

## 坡度角度检测
**功能概述：** 坡度检测区域的角度反馈。<br>
**Topic：**`perception/sensor/camera/attention_region/angle`<br>
**Msg Type s-e：**`std_msgs/msg/Float`