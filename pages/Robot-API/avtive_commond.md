# active_commond
```{toctree}
:maxdepth: 1
:glob:
```
------
Active Command Manager, which includes user SDK inputs and remote control inputs. Map the input values from the remote control into the actual inputs for the robot.


# Subscribed
|         ROS Topic          |                    Interface                     | Frame ID |       Description       |
| :------------------------: | :----------------------------------------------: | :------: | :---------------------: |
|  `command/teleop/command`  |             `sensor_msgs::msg::Joy`              |  `joy`   |     Remote control input command      |
|   `command/user/command`   | `tita_locomotion_interfaces::msg::LocomotionCmd` |   `\`    | User's SDK control command input |
| `locomotion/body/fsm_mode` |             `std_msgs::msg::String`              |   `\`    |   Actual state return of the robot    |


## Published

|        ROS Topic         |                    Interface                     | Frame ID |       Description        |
| :----------------------: | :----------------------------------------------: | :------: | :----------------------: |
| `command/active/command` | `tita_locomotion_interfaces::msg::LocomotionCmd` |  `joy`   | Control commands from external inputs to the robot |

## Config

|       Param       |      Range      | Default |                    Description                     |
| :---------------: | :-------------: | :-----: | :------------------------------------------------: |
|     `use_sdk`     |  `true/false`   | `false` |      Use SDK control, True indicates that remote control is released      |
|  `sdk_max_speed`  |      `3.0`      |  `3.0`  |              The speed limit of the machine，3.0 m/s               |
| `turn_max_speed`  |      `6.0`      |  `6.0`  |              Rotational speed limit，6.0 rad/s               |
| `pitch_max_pose`  |      `1.0`      |  `1.0`  |              The upper limit of the robot's pitch angle 1.0 rad              |
| `height_max_pose` |      `1.0`      |  `1.0`  |        The third value in the corresponding message, which is an analog value, represents the pitch angle        |
|    `pub_freq`     | `[100.0,170.0]` | `170.0` |            Active control command publication frequency                    |
| `speed_max_ratio` |   `(0.0,1.0]`   |  `1.0`  |        Corresponding to the high-speed gear button，3.0 * 1.0 = 3.0 m/s         |
| `speed_mid_ratio` |   `(0.0,1.0]`   |  `0.5`  |        Corresponding to the medium-speed gear button，3.0 * 0.5 = 1.5 m/s         |
| `speed_min_ratio` |   `(0.0,1.0]`   | `0.15`  |       Corresponding to the low-speed gear button，3.0 * 0.15 = 0.45 m/s        |
|   `height_max`    |   `(0.0,0.3]`   |  `0.3`  | Corresponding to the remote control's highest height gear, the distance between the wheel axis and the center of the body， 0.3 m |
|   `height_mid`    |   `(0.0,0.3]`   |  `0.2`  | Corresponding to the remote control's middle height gear, the distance between the wheel axis and the center of the body 0.2 m |
|   `height_min`    |   `(0.0,0.3]`   |  `0.1`  | Corresponding to the remote control's lowest height gear, the distance between the wheel axis and the center of the body 0.1 m |
