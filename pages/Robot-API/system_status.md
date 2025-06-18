# System Status Monitor


```{toctree}
:maxdepth: 1
:glob:
```

------

Description: Subscribe to data nodes from various devices within the system, assess and determine whether the data and its status are normal.

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|            ROS Topic            |            Interface             |       Frame ID       |    Description    |
| :-----------------------------: | :------------------------------: | :------------------: | :---------------: |
|  `imu_sensor_broadcaster/imu`   |     `sensor_msgs::msg::Imu`      |        `body`        |   body's IMU data   |
| `perception/camera/image/right` |    `sensor_msgs::msg::Image`     |     `right_img`      | published right camera image  |
| `perception/devices/face_point` | `sensor_msgs::msg::PointCloud2`  |        `spad`        | face_Tof Pointcloud |
| `perception/devices/neck_point` | `sensor_msgs::msg::PointCloud2`  |       `spad1`        | neck_Tof PointCloud |
|      `system/battery/left`      | `sensor_msgs::msg::BatteryState` | `left_battery_info`  |   left battery massage   |
|     `system/battery/right`      | `sensor_msgs::msg::BatteryState` | `right_battery_info` |   right battery massage    |

## Published

|          ROS Topic           |                Interface                | Frame ID | Description  |
| :--------------------------: | :-------------------------------------: | :------: | :----------: |
| `imu_sensor_broadcaster/imu` | `diagnostic_msgs::msg::DiagnosticArray` |   `/`    | system status massage |




