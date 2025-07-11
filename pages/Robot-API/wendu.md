# 内部温度调节模块

```{toctree}
:maxdepth: 1
:glob:
```

------

## Description
​	本模块用于检测机器人整机温度并调控内部解热风扇，防止温度过高导致系统崩溃。
   
   提供了一个机器人加权后的温度``Topic``和一个用于调控风扇风量的``Service``。


## Usage
```bash
source /opt/tita/ros2/setup.bash
ros2 service call /tita_namespace/system/temperature/fan_mode_set tita_system_interfaces/srv/FanModeSetSrv "{fan_mode: {data: [5]}}"
```
`data`取0为自动挡位，会根据机器人温度自动调节。
`data`取1为关闭风扇，取2～5会逐级加大风扇档位。


## Published

| ROS Topic |       Interface        | Frame ID |    Description    |
| :-------: | :--------------------: | :------: | :---------------: |
|    `system/temperature/temperature_controller`    | `sensor_msgs::msg::Temperature` |  `/weighted_temperature_info`  | 发布机器人加权后的综合温度 1Hz |

## Service

| Service Topic |     Call Interface     |    Return Interface    |       Description        |
| :-----------: | :--------------------: | :--------------------: | :----------------------: |
| `system/temperature/fan_mode_set`  | `std_msgs::msg::Byte` | `std_msgs::msg::Bool` |    一个service的案例     |



