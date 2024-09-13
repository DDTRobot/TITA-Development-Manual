# 指令调度器

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>command_manager_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	用于整合主动控制指令，与被动控制指令。将两者结合后输出最终的机器人控制指令。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|    ROS Topic    |       Interface       | Frame ID |        Description         |
| :-------------: | :-------------------: | :------: | :------------------------: |
| command/manager | sensor_msgs::msg::Joy |   Joy    | 经过消息过滤的最终控制指令 |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select command_manager_node
```

