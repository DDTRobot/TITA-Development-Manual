# Obstacle Detector

```{toctree}
:maxdepth: 1
:glob:
```
------

​	Description: The robot's obstacle detection node. ROS2 subscribes to the robot's infrared TOF sensors, and by combining the robot's posture, it calculates the obstacle distance information along the horizontal direction.  

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|            ROS Topic            |            Interface            | Frame ID |     Description     |
| :-----------------------------: | :-----------------------------: | :------: | :-----------------: |
| imu_sensor_broadcaster/imu | sensor_msgs::msg::Imu | body | Robot body IMU posture |
| perception/devices/face_point | sensor_msgs::msg::PointCloud2 | spad | Robot front face TOF sensor |
| perception/devices/neck_point | sensor_msgs::msg::PointCloud2 | spad1 | Robot lower face TOF sensor |

## Published

|              ROS Topic              |        Interface         | Frame ID |    Description     |
| :---------------------------------: | :----------------------: | :------: | :----------------: |
| perception/detector/distance_data | std_msgs::msg::Float64 | \ | Distance to the obstacle in front of the robot |
| perception/detector/angle_data | std_msgs::msg::Float64 | \ | Angle of the ground directly below the robot |

## Config

|      Param       |    Range     | Default |            Description             |
| :--------------: | :----------: | :-----: | :--------------------------------: |
| max_distance | `(0.1, 1.3)` | 1.3 | The maximum distance at which obstacle detection is effective |
| min_distance | `(0.1, 1.3)` | 0.1 | The minimum distance at which obstacle detection is effective |
| limit_xmin | `(-0.1, 0.0)` | -0.5 | The minimum range of the detected point cloud on the X-axis |
| limit_xmax | `(0.0, 1.0)` | 0.5 | The maximum range of the detected point cloud on the X-axis |
| limit_ymin | `(-0.1, 0.0)` | -0.25 | The minimum range of the detected point cloud on the Y-axis |
| limit_ymax | `(0.0, 1.0)` | 0.25 | The maximum range of the detected point cloud on the Y-axis |
| limit_zmin | `(-0.1, 0.0)` | -0.5 | The minimum range of the detected point cloud on the Z-axis |
| limit_zmax | `(0.0, 1.0)` | 0.5 | The maximum range of the detected point cloud on the Z-axis |
| pub_freq | `(0, 15)` | 15 | The publishing frequency of obstacle detection |
| obstacle_start | `true/false` | true | The switch for the node's functionality |
| obstacle_bias | `\` | 0.01 | Used for manual adjustment to compensate for sensor measurement bias |


## Build Package

```bash
# if have extra dependencies
colcon build --packages-select obstacle_detector
```

