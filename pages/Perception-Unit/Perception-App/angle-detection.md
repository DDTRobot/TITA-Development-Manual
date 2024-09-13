# 地形角度识别器

```{toctree}
:maxdepth: 1
:glob:
```
------

<p align="center"><strong>angle_detection_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	通过订阅机身的 IMU 数据解算出机器人自身的倾角，并根据tof的点云数据判断地面的倾斜程度。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Subscribed

|    ROS Topic    |           Interface           | Frame ID  |    Description    |
| :-------------: | :---------------------------: | :-------: | :---------------: |
| spad/PointCloud | sensor_msgs::msg::PointCloud2 |  spad_0   | 红外tof的点云数据 |
|    body/imu     |     sensor_msgs::msg::Imu     | base_link |   机身的IMU数据   |

## Published

|    ROS Topic     |       Interface        | Frame ID  |       Description        |
| :--------------: | :--------------------: | :-------: | :----------------------: |
| perception/angle | std_msgs::msg::Float64 | base_link | 机器人站立位置的地面角度 |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select angle_detection_node
```

