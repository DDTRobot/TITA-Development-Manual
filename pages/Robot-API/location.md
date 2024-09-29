# 机器人定位模块

```{toctree}
:maxdepth: 1
:glob:
```

------
<p align="center"><strong>tita_location</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>


<p align="center">
    语言：<!--<a href="./docs/docs_en/README_EN.md">--><strong>English</strong></a> / <strong>中文</strong>
</p>

​	为 TITA 提供里程计或定位数据，帮助机器人理解环境信息。

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribe

|           ROS Topic           |          Interface          | Frame ID |     Description     |
| :---------------------------: | :-------------------------: | :------: | :-----------------: |
| imu_sensor_broadcaster/imu | nav_msgs::msg::Odometry |  chassis_odom->base_link  | 机器人本体 Imu 数据 |
| joint_states | sensor_msgs::msg::JointState |    | 机器人关节信息 |


## Published

|           ROS Topic           |          Interface          | Frame ID |     Description     |
| :---------------------------: | :-------------------------: | :------: | :-----------------: |
| chassis/odometry | nav_msgs::msg::Odometry |  chassis_odom->base_link  | 底盘的里程计数据 |
