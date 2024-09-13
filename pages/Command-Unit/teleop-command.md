# 遥控器指令单元

```{toctree}
:maxdepth: 1
:hidden:
:glob:

Command-Unit/active-command
Command-Unit/passive-command
Command-Unit/teleop-command
Command-Unit/user-command
Command-Unit/command-manager
```

------

<p align="center"><strong>teleop_command_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	接收遥控器的控制指令，将其转为 ros2 通用的遥控器消息，发布到 `active—command` 的节点中。由于遥控器有不同厂家的按键定义，因此需要适配新的遥控器时，应当修改对应的配置文件。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|       ROS Topic       |       Interface       | Frame ID |     Description      |
| :-------------------: | :-------------------: | :------: | :------------------: |
| system/teleop_command | sensor_msgs::msg::Joy |   Joy    | 发布遥控器的控制指令 |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select teleop_command_node
```
