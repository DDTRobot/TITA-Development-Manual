# Battery System

```{toctree}
:maxdepth: 1
:glob:
```

------
## Description
This module is responsible for reading power supply data from the system, defining and implementing various power supply events and interfaces, and publishing them as `ROS2` messages into the system.

The battery device module implements the "battery data topic" and the "power management command service". Users can subscribe to the battery information topic to enhance the business logic of their own programs.


<u>**Not recommended**</u>users making any requests to the power management command service，because the power management command service is designed to respond to requests from other internal modules of the TITA robot, it is not intended to serve as a user interface.

## Preparation

Run the battery device module：
``` bash
ros2 run battery_device battery_device_node

ros2 launch battery_device battery_device_node.launch.py
```

Print battery device data：
``` bash
ros2 topic echo /your_tita_name/system/batteries/left

ros2 topic echo /your_tita_name/system/batteries/right
```

Where `your_tita_name` refers to the specific naming of the robot device, for example, `tita1234567`.


## Published

| ROS Topic |       Interface        | Frame ID | Description |
| :-------: | :--------------------: | :------: | :---------: |
| `../system/batteries/left`  | `sensor_msgs::msg::BatteryState` |  left_battery_info  |  left battery data 5Hz  |
| `../system/batteries/right`  | `sensor_msgs::msg::BatteryState` |  right_battery_info  |  right battery data 5Hz |
| `../system/battery_diagnostic/left`  | `diagnostic_msgs::msg::DiagnosticArray` |  left_battery_diagnostic_info  |  left battery diagnostic data 5Hz |
| `../system/battery_diagnostic/right`  | `diagnostic_msgs::msg::DiagnosticArray` |  right_battery_diagnostic_info  |  right battery diagnostic data 5hz |



