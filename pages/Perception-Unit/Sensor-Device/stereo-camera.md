# 双目相机模块

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>stereo_camera_device</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

​	读取双目相机设备，发布标定数据以及双目的图像信息。

## Basic Information

| Installation method | Supported platform[s]      |
| ------------------- | -------------------------- |
| Source              | Jetpack 5.1.2 , ros-humble |

------

## Published

|     ROS Topic     |          Interface           |   Frame ID    |   Description    |
| :---------------: | :--------------------------: | :-----------: | :--------------: |
|  camera/left_raw  |   sensor_msgs::msg::Image    | left_cam_raw  |   左目相机图像   |
| camera/image_raw  |   sensor_msgs::msg::Image    | right_cam_raw |   右目相机图像   |
| camera/left_info  | sensor_msgs::msg::CameraInfo | left_cam_raw  | 左目相机标定数据 |
| camera/right_info | sensor_msgs::msg::CameraInfo | right_cam_raw | 右目相机标定数据 |

## Service

| Service Topic |   Call Interface    |  Return Interface   |           Description            |
| :-----------: | :-----------------: | :-----------------: | :------------------------------: |
| camera/reset  | std_msgs::msg::Int8 | std_msgs::msg::Int8 | 重启相机的服务，返回1 则重启成功 |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select stereo_camera_device
```

