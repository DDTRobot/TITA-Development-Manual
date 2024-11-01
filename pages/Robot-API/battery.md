# 电源系统

```{toctree}
:maxdepth: 1
:glob:
```

------
## Description
本模块负责从从系统中读取电源数据，定义实现各类电源事件和接口，并以 ros2 的消息发布到系统中。

电池设备模块实现了`电池数据的话题`和`电源管理命令的服务`，用户可以订阅电池信息话题完善自己程序的业务逻辑。

<u>**不建议**</u>用户对电源管理命令的服务做任何请求，因为电源管理命令服务用于响应TITA机器人其他内部模块的请求，并非设计作为用户接口。


## Preparation

运行电池设备模块：
```
ros2 run battery_device battery_device_node
或者
ros2 launch battery_device battery_device_node.launch.py
```

打印电池设备数据：
```
ros2 topic echo /your_tita_name/system/batteries/left
或者
ros2 topic echo /your_tita_name/system/batteries/right
```

其中`your_tita_name`为具体的机器人设备命名，例如 `tita1234567`。

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Published

| ROS Topic |       Interface        | Frame ID | Description |
| :-------: | :--------------------: | :------: | :---------: |
| `../system/batteries/left`  | sensor_msgs::msg::BatteryState |  left_battery_info  |  左侧电池数据 5Hz  |
| `../system/batteries/right`  | sensor_msgs::msg::BatteryState |  right_battery_info  |  右侧电池数据 5Hz |
| `../system/battery_diagnostic/left`  | diagnostic_msgs::msg::DiagnosticArray |  left_battery_diagnostic_info  |  左侧电池诊断数据 5Hz |
| `../system/battery_diagnostic/right`  | diagnostic_msgs::msg::DiagnosticArray |  right_battery_diagnostic_info  |  右侧电池诊断数据 5hz |


## Build Package

```bash
# If you haven't installed can-utils
# apt-get install can-utils
colcon build --merge-install --packages-select battery_device
```
---
# 电源控制器

## Description
​	电源控制器是基于电池设备模块的上层管理模块，主要负责机器人的电源事件逻辑管理。
电源控制器实现了一个用于`关闭整机电源的服务`，一旦响应请求，将会立即关闭机器人所有电源，**不会等待机器人是否处于安全状态**。

请注意，**这个接口并非设计给用户使用的，不建议用这个服务实现所谓“急停”意义的功能**，因此不建议用户对这个服务做任何请求，因为这个接口被设计给机器人内部模块的系统管理层。

## Preparation

运行电源控制器模块：
```
ros2 run power_controller power_controller_node 
或者
ros2 launch power_controller power_controller_node.launch.py
```


## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

| ROS Topic |       Interface        | Frame ID | Description |
| :-------: | :--------------------: | :------: | :---------: |
| `system/battery/left`  | sensor_msgs::msg::BatteryState |  left_battery_info  |  接收左侧电池数据  |
| `system/battery/right`  | sensor_msgs::msg::BatteryState |  right_battery_info  |  接收右侧电池数据  |

## Service

| Service Topic |   Service Interface    |       Description        |
| :-----------: | :--------------------: | :----------------------: |
| service name | std_srvs::srv::Trigger |    关机触发服务     |

## Client

| Client Topic |   Client Interface    |       Description        |
| :-----------: | :--------------------: | :----------------------: |
| service name | tita_system_interfaces::srv::PowerStateSetSrv |    请求设置电源状态客户端     |
| service name | tita_system_interfaces::srv::PowerHeartBeatSrv |    请求电源心跳包客户端     |
| service name | tita_system_interfaces::srv::PowerSelfTestSrv |    请求电源状态自检客户端     |

