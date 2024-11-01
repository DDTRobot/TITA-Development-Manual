# 系统状态监测器

```{toctree}
:maxdepth: 1
:glob:
```

------

功能描述：订阅系统各个设备的数据节点，评估判断数据以及数据状态是否正常。

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|            ROS Topic            |            Interface             |       Frame ID       |    Description    |
| :-----------------------------: | :------------------------------: | :------------------: | :---------------: |
|  `imu_sensor_broadcaster/imu`   |     `sensor_msgs::msg::Imu`      |        `body`        |   机身的IMU数据   |
| `perception/camera/image/right` |    `sensor_msgs::msg::Image`     |     `right_img`      | 发布右目相机图像  |
| `perception/devices/face_point` | `sensor_msgs::msg::PointCloud2`  |        `spad`        | 前脸Tof传感器点云 |
| `perception/devices/neck_point` | `sensor_msgs::msg::PointCloud2`  |       `spad1`        | 下方Tof传感器点云 |
|      `system/battery/left`      | `sensor_msgs::msg::BatteryState` | `left_battery_info`  |   左侧电池信息    |
|     `system/battery/right`      | `sensor_msgs::msg::BatteryState` | `right_battery_info` |   右侧电池信息    |

## Published

|          ROS Topic           |                Interface                | Frame ID | Description  |
| :--------------------------: | :-------------------------------------: | :------: | :----------: |
| `imu_sensor_broadcaster/imu` | `diagnostic_msgs::msg::DiagnosticArray` |   `/`    | 系统状态信息 |


