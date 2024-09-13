# 机器人运动控制模块

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>ros2_control</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>
​	使用 [ros2_control](https://github.com/ros-controls/ros2_control) 框架实现的运动控制。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

| ROS Topic  |        Interface         | Frame ID |     Description      |
| :--------: | :----------------------: | :------: | :------------------: |
|    /tf     | tf2_msgs::msg::TFMessage |   None   |     机器人的tf树     |
| /tf_static | tf2_msgs::msg::TFMessage |   None   | tf树中的静态关节描述 |

## Subscribed

|  ROS Topic   |          Interface           | Frame ID  |  Description   |
| :----------: | :--------------------------: | :-------: | :------------: |
| system/joint | sensor_msgs::msg::JointState |   None    | 关节电机的数据 |
|   body/imu   |    sensor_msgs::msg::Imu     | base_link | 机身的IMU数据  |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select ...
```

