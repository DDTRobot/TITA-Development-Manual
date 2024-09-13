# 状态控制器

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>robot_state_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	机器人的设备状态监视器，用于检查当前机器人所有硬件状态是否正常。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|   ROS Topic   |               Interface                | Frame ID  |         Description         |
| :-----------: | :------------------------------------: | :-------: | :-------------------------: |
| system/status | diagnostic_msgs::msg::DiagnosticStatus | base_link | 对应base_link的所属设备状态 |

## Subscribed

|       ROS Topic        |               Interface                |     Frame ID     |           Description            |
| :--------------------: | :------------------------------------: | :--------------: | :------------------------------: |
|     system/status      | diagnostic_msgs::msg::DiagnosticStatus |    base_link     |   对应base_link的所属设备状态    |
|    spad/PointCloud     |     sensor_msgs::msg::PointCloud2      |      spad_0      | 多点测距的tof还原的点云15 Hz发布 |
|    camera/left_raw     |        sensor_msgs::msg::Image         |   left_cam_raw   |           左目相机图像           |
| ultrasonic_front/topic |         sensor_msgs/msg/Range          | ultrasonic_front |     超声波测量结果 30 Hz发布     |
|   system/JointState    |      sensor_msgs::msg::JointState      |       None       |     发布的电机数据关节信息。     |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select robot_state_node
```
