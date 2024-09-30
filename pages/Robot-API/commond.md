# 指令管理模块

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>command_manager</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>

<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	指令管理模块，用于整合主动指令与被动指令，将其统一后下发至机器人。

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|         ROS Topic         |                    Interface                     |   Frame ID    |   Description    |
| :-----------------------: | :----------------------------------------------: | :-----------: | :--------------: |
| `command/active/command`  | `tita_locomotion_interfaces::msg::LocomotionCmd` |     `joy`     | 主动消息控制指令 |
| `command/passive/command` | `tita_locomotion_interfaces::msg::LocomotionCmd` | `passive_joy` | 被动消息控制指令 |

## Published

|          ROS Topic          |             Interface             | Frame ID |        Description         |
| :-------------------------: | :-------------------------------: | :------: | :------------------------: |
| `command/manager/cmd_twist` |    `geometry_msgs::msg::Twist`    |   `/`    | 机器人底盘运动最终控制指令 |
| `command/manager/cmd_pose`  | `geometry_msgs::msg::PoseStamped` |   `/`    | 机器人主体姿态最终控制指令 |
|  `command/manager/cmd_key`  |      `std_msgs::msg::String`      |   `/`    |   机器人状态最终控制指令   |

## Build Package

```bash
# apt install ros-humble-joy
colcon build --packages-select command_manager tita_locomotion_interfaces
```

