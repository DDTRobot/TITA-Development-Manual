# 传感器模块

```{toctree}
:maxdepth: 1
:glob:
```

------
传感器包括红外Tof、超声模块、双目相机模块；将提供对应的API进行二次开发

<p align="center"><strong>dual_tof_device</strong></p>


​	红外 TOF 的数据发布，将多点测距的 TOF 转为点云数据发布到 ROS 中。

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Published

|           ROS Topic           |          Interface          | Frame ID |     Description     |
| :---------------------------: | :-------------------------: | :------: | :-----------------: |
| perception/devices/face_point | sensor_msgs/msg/PointCloud2 |  spad_0  | 发布面部TOF点云数据 |
| perception/devices/neck_point | sensor_msgs/msg/PointCloud2 |  spad_1  | 发布颈部TOF点云数据 |



## Build Package

```bash
# if have extra dependencies
apt install libpcl-dev
colcon build --packages-select dual_tof_device
```
---
<p align="center"><strong>ultrawave_device</strong></p>

​	这是一个超声波模块的设备节点，用于读取超声波模块的数据，并发布出来。该功能未是完成体，仍在在持续更新中。 

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Published

|          ROS Topic           |       Interface       |     Frame ID     |       Description        |
| :--------------------------: | :-------------------: | :--------------: | :----------------------: |
| `perception/devices/ultrawave` | `sensor_msgs/msg/Range` | ultrasonic_front | 超声波测量结果 30 Hz发布 |



## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select ultrawave_device
```
---
<p align="center"><strong>stereo_camera_device</strong></p>


​	这是一个双目相机的设备节点，用于读取双目相机的数据，并发布出来。该功能未是完成体，仍在在持续更新中。

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Published

|           ROS Topic           |         Interface          |    Frame ID     |     Description      |
| :---------------------------: | :------------------------: | :-------------: | :------------------: |
| `perception/camera/image/left`  |   `sensor_msgs/msg/Image`    | left_frame_raw  |   发布左目相机图像   |
| `perception/camera/image/right` |   `sensor_msgs/msg/Image`    | right_frame_raw |   发布右目相机图像   |
|  `perception/camera/info/left`  | `sensor_msgs/msg/CameraInfo` | left_frame_raw  | 发布左目相机标定数据 |
| `perception/camera/info/right` | `sensor_msgs/msg/CameraInfo` | right_frame_raw | 发布右目相机标定数据 |



