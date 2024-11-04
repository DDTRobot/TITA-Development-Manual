# Sensor Unit

```{toctree}
:maxdepth: 1
:glob:
```

------
Sensors include infrared ToF, ultrasonic modules, and binocular camera modules; corresponding APIs will be provided for secondary development.

## dual_tof_device


​	Infrared ToF data publishing involves converting the distance measurements from a multi-point ToF into point cloud data and publishing it to ROS.



#### Published

|           ROS Topic           |          Interface          | Frame ID |     Description     |
| :---------------------------: | :-------------------------: | :------: | :-----------------: |
| `perception/devices/face_point` | `sensor_msgs/msg/PointCloud2` |  `spad_0`  | Face Tof Pointcloud data |
| `perception/devices/neck_point` | `sensor_msgs/msg/PointCloud2` |  `spad_1`  | Neck Tof Pointcloud data |




## ultrawave_device

​This is a device node for an ultrasonic module, used to read data from the ultrasonic module and publish it. This feature is not yet complete and is still being continuously updated.



#### Published

|          ROS Topic           |       Interface       |     Frame ID     |       Description        |
| :--------------------------: | :-------------------: | :--------------: | :----------------------: |
| `perception/devices/ultrawave` | `sensor_msgs/msg/Range` | `ultrasonic_front` | Ultrasonic measurement results, published by 30 Hz |


## stereo_camera_device


This is a device node for a binocular camera, used to read data from the binocular camera and publish it. This feature is not yet complete and is still being continuously updated.


## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Published

|           ROS Topic           |         Interface          |    Frame ID     |     Description      |
| :---------------------------: | :------------------------: | :-------------: | :------------------: |
| perception/camera/image/left  |   sensor_msgs/msg/Image    | left_frame_raw  |   Publish the left camera image   |
| perception/camera/image/right |   sensor_msgs/msg/Image    | right_frame_raw |   Publish the right camera image   |
|  perception/camera/info/left  | sensor_msgs/msg/CameraInfo | left_frame_raw  | Publish the calibration data of the left camera |
| perception/camera/info/right  | sensor_msgs/msg/CameraInfo | right_frame_raw | Publish the calibration data of the right camera  |

