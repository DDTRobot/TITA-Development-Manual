# Passive commond unit

```{toctree}
:maxdepth: 1
:glob:
```

------


Description: The passive command module is designed to receive sensor information and convert it into restrictions on user-initiated control commands. This allows the robot's input commands to be influenced by environmental information, thereby serving to protect the robot.

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|              ROS Topic              |        Interface         | Frame ID |   Description    |
| :---------------------------------: | :----------------------: | :------: | :--------------: |
| `perception/obstacle/distance_data` | `std_msgs::msg::Float64` |   `/`    | Recognized obstacle distance|

## Published

|         ROS Topic         |                    Interface                     |   Frame ID    |           Description            |
| :-----------------------: | :----------------------------------------------: | :-----------: | :------------------------------: |
| `command/passive/command` | `tita_locomotion_interfaces::msg::LocomotionCmd` | `passive_joy` | Used to describe the current maximum motion capabilities of the robot.
 |

## Build Package

```bash
# apt install ros-humble-joy
colcon build --packages-select passive_command
```

