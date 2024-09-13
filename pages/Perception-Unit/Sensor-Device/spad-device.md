# 红外TOF模块

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>spad_deivce</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>

<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	多点红外TOF，发布的数据信息。根据器件描述，将极坐标系下的测距信息转换为直角坐标系下的点云信息。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|    ROS Topic    |           Interface           | Frame ID |           Description            |
| :-------------: | :---------------------------: | :------: | :------------------------------: |
| spad/PointCloud | sensor_msgs::msg::PointCloud2 |  spad_0  | 多点测距的tof还原的点云15 Hz发布 |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select spad_deivce
```

