# 视觉里程计

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>visual_slam_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>

<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	视觉里程计及建立用于触发回环检测的 landmark 地图。给机器人一个准确的里程计信息而不是定位信息。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|   ROS Topic    |           Interface           |      Frame ID       |       Description        |
| :------------: | :---------------------------: | :-----------------: | :----------------------: |
| vslam/Odometry |    nav_msgs::msg::Odometry    | odom \| camera_link | 纯VO状态下的里程计 60 hz |
| vslam/PointMap | sensor_msgs::msg::PointCloud2 |        odom         |  vslam的landmark 10 hz   |

## Subscribed

|     ROS Topic     |          Interface           |   Frame ID    |   Description    |
| :---------------: | :--------------------------: | :-----------: | :--------------: |
|  camera/left_raw  |   sensor_msgs::msg::Image    | left_cam_raw  |   左目相机图像   |
| camera/image_raw  |   sensor_msgs::msg::Image    | right_cam_raw |   右目相机图像   |
| camera/left_info  | sensor_msgs::msg::CameraInfo | left_cam_raw  | 左目相机标定数据 |
| camera/right_info | sensor_msgs::msg::CameraInfo | right_cam_raw | 右目相机标定数据 |

## Service

| Service Topic |                  Call Interface                   |    Return Interface    |    Description    |
| :-----------: | :-----------------------------------------------: | :--------------------: | :---------------: |
| service name  | std_msgs::msg::Float64  ｜ std_msgs::msg::Float64 | std_msgs::msg::Float64 | 一个service的案例 |



## Build Package

```bash
# if have extra dependencies
apt install libopencv-dev
apt install libpcl-dev
colcon build --packages-select visual_slam_node
```

