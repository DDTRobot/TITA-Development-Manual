## Perception Message API
感知信息包括相机图像、标定，IMU、Tof等数据，在后续二次开发中可以通过以上这些接口进行数据获取和调用。

### API明细

#### 轮式里程计

**功能概述**：融合IMU且进行位姿优化的里程计。不可记录Z信息

**Topic**： `/tita_spacename/chassis/odometry`

**Msg Type**：`nav_msgs/msg/Odometry`

#### 姿态重置

**功能概述：** 重置机器人底盘姿态

**Service：** `/tita_spacename/chassis/srv/reset`

**命令示例：**`ros2 service call /tita_spacename/chassis/srv/reset std_srvs/srv/Trigger {}`

#### 相机图像

**功能概述：** 发布相机去畸变后的彩色图像 60hz。
**Topic：**
`perception/camera/image/left`
`perception/camera/image/right`

**Msg Type：** sensor_msgs/msg/Image

#### 相机标定数据

**功能概述：** 发布相机标定数据 频率60hz。

**Topic：**
`perception/camera/info/left`
`perception/camera/info/right`

**Msg Type：** `sensor_msgs/msg/CameraInfo`

#### 坡度角度检测

**功能概述：** 坡度检测区域的角度反馈。

**Topic：**
`/tita4265492/perception/detector/angle_data`

**Msg Type：** `std_msgs/msg/Float64`

#### 障碍物距离检测

**功能概述：** 障碍物距离检测区域的距离反馈。

**Topic：**
`/tita_spacename/perception/obstacle/distance_data`

**Msg Type：** `std_msgs/msg/Float64`

#### 障碍物检测

**功能概述：** 障碍物检测区域的障碍物信息反馈。

**Topic：**
`/tita_spacename/perception/obstacle/point`

**Msg Type：** `sensor_msgs/msg/PointCloud2`

#### 上下TOF识别点云

**功能概述：** 发布Tof识别点云。

**Topic：**
`/tita_spacename/perception/devices/face_point`
`/tita_spacename/perception/devices/neck_point`

**Msg Type：** `sensor_msgs/msg/PointCloud2`
