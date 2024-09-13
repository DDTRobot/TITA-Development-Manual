# 被动指令控制器

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>passive_command_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	接收传感器的识别结果与机器人的状态指令，转为当前状态下可以使用的指令及其可用的数值范围。如速度上限，某些按键是否可用。将其发布到 `command-manager` 的节点中。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|       ROS Topic        |       Interface       | Frame ID |                Description                 |
| :--------------------: | :-------------------: | :------: | :----------------------------------------: |
| system/passive_command | sensor_msgs::msg::Joy |   Joy    | 机器人当前的状态整合，发布的运控规则限制器 |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select passive_command_node
```

