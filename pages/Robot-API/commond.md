# Commond Unit

```{toctree}
:maxdepth: 1
:glob:
```

------
​**Description**: The Command Management Module is designed to integrate both active and passive commands, and then unify them before sending them down to the robot.


## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed

|         ROS Topic         |                    Interface                     |   Frame ID    |   Description    |
| :-----------------------: | :----------------------------------------------: | :-----------: | :--------------: |
| `command/active/command`  | `tita_locomotion_interfaces::msg::LocomotionCmd` |     `joy`     | active commond |
| `command/passive/command` | `tita_locomotion_interfaces::msg::LocomotionCmd` | `passive_joy` | passive commond |

## Published

|          ROS Topic          |             Interface             | Frame ID |        Description         |
| :-------------------------: | :-------------------------------: | :------: | :------------------------: |
| `command/manager/cmd_twist` |    `geometry_msgs::msg::Twist`    |   `/`    | Robot chassis motion final control commands |
| `command/manager/cmd_pose`  | `geometry_msgs::msg::PoseStamped` |   `/`    | Final control commands for the robot's main body posture |
|  `command/manager/cmd_key`  |      `std_msgs::msg::String`      |   `/`    |   Final control commands for the robot's status   |

## Build Package

```bash
# apt install ros-humble-joy
colcon build --packages-select command_manager tita_locomotion_interfaces
```

