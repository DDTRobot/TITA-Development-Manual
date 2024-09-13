# 障碍检测器

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>obstacle_detection_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	这是一个障碍检测节点。根据传感器的获取的环境信息和 tf 树之间的坐标系转换，还原出机器人前方的障碍信息。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Subscribed

|    ROS Topic    |           Interface           | Frame ID |    Description    |
| :-------------: | :---------------------------: | :------: | :---------------: |
| spad/PointCloud | sensor_msgs::msg::PointCloud2 |  spad_0  | 红外tof的点云数据 |

## Published

|        ROS Topic         |           Interface           | Frame ID  |    Description     |
| :----------------------: | :---------------------------: | :-------: | :----------------: |
| spad/obstacle/PointCloud | sensor_msgs::msg::PointCloud2 | base_link | 障碍部分的点云信息 |
|    spad/obstacle/data    |    std_msgs::msg::Float64     | base_link |     障碍的距离     |

## Param

|  Param Name  |     Default Value      |    Description     |
| :----------: | :--------------------: | :----------------: |
| service name | std_msgs::msg::Float64 | 检测障碍的限制条件 |


## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select obstacle_detection_node
```

