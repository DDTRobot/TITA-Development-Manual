# 网络控制器

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>wifi_control_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	该仓库参考了[wifi_ddwrt](https://github.com/ros-drivers/wifi_ddwrt/tree/noetic-devel) 的消息格式，在 ros2 中做了实现。提供了关于 AP 模式开关，和 wifi 管理的 ROS2 

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

| ROS Topic | Interface | Frame ID | Description |
| :-------: | :-------: | :------: | :---------: |
|           |           |          |             |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select wifi_control_node
```
