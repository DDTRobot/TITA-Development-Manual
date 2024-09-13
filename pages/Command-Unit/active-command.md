# 主动指令控制器

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>active_manager_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	将接收的遥控器指令、`SDK` 控制指令转为 `ROS2` 的消息发布到 `command-manager` 的节点中。管理主动的指令消息，当指令发生冲突时，对指令进行判定和切换。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|   ROS Topic    |       Interface       | Frame ID |      Description       |
| :------------: | :-------------------: | :------: | :--------------------: |
| active/Command | sensor_msgs::msg::Joy |   Joy    | 发布控制机器人的状态量 |

## Subscribed

|       ROS Topic       |       Interface       | Frame ID |     Description      |
| :-------------------: | :-------------------: | :------: | :------------------: |
|     user/Command      | sensor_msgs::msg::Joy |   Joy    |    用户的控制指令    |
| system/teleop_command | sensor_msgs::msg::Joy |   Joy    | 发布遥控器的控制指令 |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select active_manager_node
```
