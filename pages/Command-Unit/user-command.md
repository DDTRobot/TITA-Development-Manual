# 用户控制指令节点

```{toctree}
:maxdepth: 2
:glob:
```

------

<p align="center"><strong>user_command_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	用户的 `SDK` 开发接口，将用户的指令转为 ros2 的通用遥控器 `active—command` 的节点中。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|  ROS Topic   |       Interface       | Frame ID |   Description   |
| :----------: | :-------------------: | :------: | :-------------: |
| user/Command | sensor_msgs::msg::Joy |   Joy    | 用户的 sdk 指令 |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select user_command_node
```
