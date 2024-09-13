# 导航路径规划模块

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>navigation_plan_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	将点云转换为东北天坐标系，触发导航路径规划的 srv 中，将根据配置的参数，返回一条可以行进的路线。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Param

|   Param Name    | Default Value |           Description           |
| :-------------: | :-----------: | :-----------------------------: |
|   limit_min_z   |     -1.0      | z轴向大于此数值的全部定义为障碍 |
|   limit_max_z   |      3.0      | z轴向小于此数值的全部定义为障碍 |
|  per_box_size   |      0.1      |   导航用的二维 Grid 的分辨率    |
| robot_body_size |      0.5      |      机器人的体积占用情况       |

## Service

| Service Topic |        Call Interface         |  Return Interface   |             Description              |
| :-----------: | :---------------------------: | :-----------------: | :----------------------------------: |
| find_path/srv | sensor_msgs::msg::PointCloud2 | nav_msgs::msg::Path | 根据输入的点云与坐标返回一条可行轨迹 |
|               | geometry_msgs/msg/Point Start |                     |              起始坐标点              |
|               |  geometry_msgs/msg/Point End  |                     |              终止坐标点              |



## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select navigation_plan_node
```

