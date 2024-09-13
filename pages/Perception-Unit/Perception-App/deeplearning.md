# 深度学习模块

```{toctree}
:maxdepth: 1
:glob:
```
------

<p align="center"><strong>deeplearning_node</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	其中包含了各种模型的推理。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## 一、双目深度估计

### Published

|     ROS Topic     |           Interface           |   Frame ID   |           Description            |
| :---------------: | :---------------------------: | :----------: | :------------------------------: |
| camera/PointCloud | sensor_msgs::msg::PointCloud2 | left_cam_raw | 深度估计得到的彩色点云数据 10 hz |

### Subscribed

|     ROS Topic     |          Interface           |   Frame ID    |   Description    |
| :---------------: | :--------------------------: | :-----------: | :--------------: |
|  camera/left_raw  |   sensor_msgs::msg::Image    | left_cam_raw  |   左目相机图像   |
| camera/image_raw  |   sensor_msgs::msg::Image    | right_cam_raw |   右目相机图像   |
| camera/left_info  | sensor_msgs::msg::CameraInfo | left_cam_raw  | 左目相机标定数据 |
| camera/right_info | sensor_msgs::msg::CameraInfo | right_cam_raw | 右目相机标定数据 |



## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select deeplearning_node
```

