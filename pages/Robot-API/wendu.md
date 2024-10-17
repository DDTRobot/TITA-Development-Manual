# Internal temperature regulation module

```{toctree}
:maxdepth: 1
:glob:
```

------

## Description
​This module is used to detect the overall temperature of the robot and control the internal cooling fan to prevent system crashes due to excessive temperatures.

It provides a `Topic` for the robot's weighted temperature and a `Service` for controlling the fan's airflow.

## Preparation
Run temperature controller：
```bash
ros2 run temperature_controller temperature_controller_node
or
ros2 launch temperature_controller temperature_controller.launch.py
```

## Usage
```bash
ros2 service call /system/temperature/fan_mode_set tita_system_interfaces/srv/FanModeSetSrv "{fan_mode: {data: 0x01}}"
```
Setting data to 0 will engage the automatic gear, which will adjust the fan speed based on the robot's temperature.

Setting data to 1 turns off the fan, while setting data to 2 through 5 will progressively increase the fan speed in increments.

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Published

| ROS Topic |       Interface        | Frame ID |    Description    |
| :-------: | :--------------------: | :------: | :---------------: |
|    system/temperature/temperature_controller    | sensor_msgs::msg::Temperature |  /weighted_temperature_info  | Publish the comprehensive weighted temperature of the robot at 1Hz. |

## Service

| Service Topic |     Call Interface     |    Return Interface    |       Description        |
| :-----------: | :--------------------: | :--------------------: | :----------------------: |
| system/temperature/fan_mode_set  | std_msgs::msg::Byte | std_msgs::msg::Bool |    one case of service     |



## Build Package

```bash
# If you haven't installed can-utils
# apt-get install can-utils
colcon build --merge-install --packages-select temperature_controller 
