# 超声波测距模块

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>ultrasonic_wave_device</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>

<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	这是一个超声波模块的设备节点，用于读取超声波模块的数据，并发布出来。 

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|       ROS Topic        |       Interface       |     Frame ID     |       Description        |
| :--------------------: | :-------------------: | :--------------: | :----------------------: |
| ultrasonic_front/topic | sensor_msgs/msg/Range | ultrasonic_front | 超声波测量结果 30 Hz发布 |



## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select ultrasonic_wave_device
```

