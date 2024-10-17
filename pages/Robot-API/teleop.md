# Remote Control Command Module

```{toctree}
:maxdepth: 1
:glob:
```

------

​	Description: Used to parse the data from the receiver and dynamically set the parameters for various functional modules. This node can modify the mapping relationship of buttons by changing the configuration file.

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|       ROS Topic        |            Interface             |       Frame ID       |       Description        |
| :--------------------: | :------------------------------: | :------------------: | :----------------------: |
|         `/joy`         |     `sensor_msgs::msg::Joy`      |        `joy`         | For receiving nodes from third-party remote controllers |
| `system/battery/left`  | `sensor_msgs::msg::BatteryState` | `left_battery_info`  |  Remote Control Displaying Left Battery Information |
| `system/battery/right` | `sensor_msgs::msg::BatteryState` | `right_battery_info` |  Remote Control Displaying Right Battery Information  |

## Published

|        ROS Topic         |        Interface        | Frame ID |              Description               |
| :----------------------: | :---------------------: | :------: | :------------------------------------: |
| `command/teleop/command` | `sensor_msgs::msg::Joy` |  `joy`   | Publish the message to change the button order to `active_command`|
|          `/joy`          | `sensor_msgs::msg::Joy` |  `joy`   |        Publish data to the Joy message interface        |

## Config
| Param        | Range          | Default | Description                             |
|--------------|----------------|---------|-----------------------------------------|
| DebugMode    | true/false     | false   | Debugging using switches                         |
| AxesSize     | 1-8            | 8       |The number of processed keys             |
| MoveAxes     | a/b \| 0-7     | a0      | Corresponding to the first numerical value in the message, analog quantity, forward axis   |
| TurnAxes     | a/b \| 0-7     | a1      | Corresponding to the second numerical value in the message, analog quantity, steering axis   |
| PitchAxes    | a/b \| 0-7     | a2      | Corresponding to the third numerical value in the message, analog quantity, pitch angle   |
| RollAxes     | a/b \| 0-7     | a3      | Corresponding to the fourth numerical value in the message, analog quantity, roll axis   |
| StandUp      | a/b \| 0-7     | b4      | orresponding to the fifth numerical value in the message, switch quantity, standing switch |
| HeightSwitch | a/b \| 0-7     | b5      | Corresponding to the sixth numerical value in the message, switch quantity, height adjustment  |
| JumpButton   | a/b \| 0-7     | b6      | Corresponding to the seventh numerical value in the message, switch quantity, jump switch |
| SpeedButton  | a/b \| 0-7     | b7      | Corresponding to the eighth numerical value in the message, switch quantity, speed adjustment  |
| AxesBias     | float       | 0.0013  | Dead zone range of the remote control analog axis              |

## Build Package

```bash
# apt install ros-humble-joy
colcon build --packages-select teleop_command
```

