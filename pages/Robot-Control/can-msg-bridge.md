# 通信消息桥

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>can_msg_bridge</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>
​	负责解析  mcu-controller 提供的数据，同步 MCU 数据与上层系统的时间戳，将其转发给 robot-controller 。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|  ROS Topic   |          Interface           | Frame ID  |      Description      |
| :----------: | :--------------------------: | :-------: | :-------------------: |
| system/joint | sensor_msgs::msg::JointState |   None    |    关节电机的数据     |
|   body/imu   |    sensor_msgs::msg::Imu     | base_link | 机器人本体的 IMU 数据 |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select can_msg_bridge
```
