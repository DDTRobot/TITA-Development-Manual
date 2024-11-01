# 障碍检测器

```{toctree}
:maxdepth: 1
:glob:
```
------

​	功能描述：机器人对障碍物检测节点。ROS2 订阅机器人的红外 TOF 传感器，结合机器人的姿态，求出机器人沿水平方向的障碍距离信息。  

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|            ROS Topic            |            Interface            | Frame ID |     Description     |
| :-----------------------------: | :-----------------------------: | :------: | :-----------------: |
|  `imu_sensor_broadcaster/imu`   |     `sensor_msgs::msg::Imu`     |  `body`  |     机身IMU姿态     |
| `perception/devices/face_point` | `sensor_msgs::msg::PointCloud2` |  `spad`  | 机器人前脸TOF传感器 |
| `perception/devices/neck_point` | `sensor_msgs::msg::PointCloud2` | `spad1`  | 机器人下方TOF传感器 |

## Published

|              ROS Topic              |        Interface         | Frame ID |    Description     |
| :---------------------------------: | :----------------------: | :------: | :----------------: |
| `perception/detector/distance_data` | `std_msgs::msg::Float64` |   `\`    | 机器人前方障碍距离 |
|  `perception/detector/angle_data`   | `std_msgs::msg::Float64` |   `\`    | 机器人下方地面角度 |

## Config

|      Param       |    Range     | Default |            Description             |
| :--------------: | :----------: | :-----: | :--------------------------------: |
|  `max_distance`  | `(0.1,1.3)`  |  `1.3`  |       障碍检测生效的最远距离       |
|  `min_distance`  | `(0.1,1.3)`  |  `0.1`  |       障碍检测生效的最近距离       |
|   `limit_xmin`   | `(-0.1,0.0)` | `-0.5`  |     检测点云 X 轴，的最小范围      |
|   `limit_xmax`   | `(0.0,1.0)`  |  `0.5`  |     检测点云 X 轴，的最大范围      |
|   `limit_ymin`   | `(-0.1,0.0)` | `-0.25` |     检测点云 Y 轴，的最小范围      |
|   `limit_ymax`   | `(0.0,1.0)`  | `0.25`  |     检测点云 Y 轴，的最大范围      |
|   `limit_zmin`   | `(-0.1,0.0)` | `-0.5`  |     检测点云 Z 轴，的最小范围      |
|   `limit_zmax`   | `(0.0,1.0)`  |  `0.5`  |     检测点云 Z 轴，的最大范围      |
|    `pub_freq`    |   `(0,15)`   |  `15`   |         障碍检测的发布频率         |
| `obstacle_start` | `true|false` | `true`  |            节点功能开关            |
| `obstacle_bias`  |     `\`      | `0.01`  | 用于手动调整，补偿传感器的测量偏差 |



