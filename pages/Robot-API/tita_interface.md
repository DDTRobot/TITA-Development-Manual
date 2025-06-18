# TITA-Interface

```{toctree}
:maxdepth: 1
:glob:
```

------

<p align="center"><strong>tita_locomotion_interfaces</strong></p>


​	Description:Custom message interface related to robot motion control.

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## LocomotionCmd.msg

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
|   `std_msgs/Header`   |  `header`  |     ROS2 Standard Message Header      |
|       `string`        | `fsm_mode` |        Robot Status        |
| `geometry_msgs/Pose`  |   `pose`   | Posture control information for the robot's torso |
| `geometry_msgs/Twist` |  `twist`   | Velocity control information for the robot's chassis |

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select tita_locomotion_interfaces
```
---

<p align="center"><strong>tita_perception_interfaces</strong></p>

​	Description:Custom interfaces related to robot perception.


## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## BoundingBox.msg

|       Type        |   Name   |       Description        |
| :---------------: | :------: | :----------------------: |
| `std_msgs/Header` | `header` |     ROS2 Standard Message       |
|     `float64`     | `x_min`  | Minimum value of x in the bounding box. |
|     `float64`     | `y_min`  | Minimum value of y in the bounding box. |
|     `float64`     | `x_max`  | Maximum value of x in the bounding box. |
|     `float64`     | `y_max`  | Maximum value of y in the bounding box |
|     `string`      | `label`  |         Identification ID          |

## BoundingBox.msg

|       Type        |   Name   |          Description           |
| :---------------: | :------: | :----------------------------: |
| `std_msgs/Header` | `header` |         ROS2 Standard Message        |
|  `BoundingBox[]`  | `boxes`  | An array composed of bounding box messages |

## ObjectDetection.srv

|        Type         |   Name   |   Description    |
| :-----------------: | :------: | :--------------: |
| `sensor_msgs/Image` | `image`  | request to send a picture |
| `BoundingBoxArray`  | `result` |   Return the recognition results |

## 

## Build Package

```bash
# if have extra dependencies
# apt install <libdepend-dev>
colcon build --packages-select tita_perception_interfaces
```
---
<p align="center"><strong>tita_system_interfaces</strong></p>

Description:Custom message interface related to robot system control.
## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## FanModeSetSrv.srv

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
|   `std_msgs/Byte`   |  `fan_mode`  |     Fan mode      |
| `bool` |  `success`   | return result |

风扇模式取值：

| fan_mode | Description |
| :--: | :---------: |
|  0   | Automatic mode   |
|  1   | Turn off fan   |
|  2   | Speed level 1   |
|  3   | Speed level 2   |
|  4   | Speed level 3   |
|  5   | Speed level 4   |

## HeadLightControlSrv.srv

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
bool | is_control | Take control |
| uint32[48] | light_rgbl_value | Light bead RGBL value |
| bool | success | Return result |

**the value for take control：**

| is_control | Description |
| :--: | :---------: |

| false | Relinquish control |
| true | Take control |

**Light bead RGBL value range:**

| light_rgbl_value | Description |
| :--: | :---------: |
| uint32[0] | RGBL value of the first light bead |
| uint32[1] | RGBL value of the second light bead |
| uint32[2] | RGBL value of the third light bead |
| uint32[...] | Omitted |
| uint32[45] | RGBL value of the forty-fifth light bead |
| uint32[46] | RGBL value of the forty-sixth light bead |
| uint32[47] | RGBL value of the forty-seventh light bead |

**Assuming uint32[0] = 0x12345678, the specific meaning of the RGBL values 
for the first LED bead is:**

| uint32[0] | Description |
| :--: | :---------: |
| 0x12 | The Red value for the first LED bead is set to 0x12, with a range of 0x00 to 0xFF. |
| 0x34 | The Green value for the first LED bead is set to 0x34, with a range of 0x00 to 0xFF. |
| 0x56 | The Blue value for the first LED bead is set to 0x56, with a range of 0x00 to 0xFF. |
| 0x78 | The Lightness value for the first LED bead is set to 0x78, with a range of 0x00 to 0xFF. |

The meaning of the values for the other LED beads follows the same logic.

## TailLightControlSrv.srv

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
bool | is_control | Take control |
| uint32[48] | light_rgbl_value | Light bead RGBL value |
| bool | success | Return result |

**the value for take control：**

| is_control | Description |
| :--: | :---------: |
| false | Relinquish control |
| true | Take control |

**Light bead RGBL value range:**

| light_rgbl_value | Description |
| :--: | :---------: |
| uint32[0] | The RGBL value for the first LED bead |
| uint32[1] | The RGBL value for the second LED bead |
| uint32[2] | The RGBL value for the third LED bead |
| uint32[...] | Omitted |
| uint32[33] | The RGBL value for the thirty-third LED bead |
| uint32[34] | The RGBL value for the thirty-fourth LED bead |
| uint32[35] | The RGBL value for the thirty-fifth LED bead |

**Assuming uint32[0] = 0x12345678, the specific meaning of the RGBL values 
for the first LED bead is:**

| uint32[0] | Description |
| :--: | :---------: |
| 0x12 | The Red value for the first LED bead is 0x12, with a range of 0x00 to 0xFF. |
| 0x34 | The Green value for the first LED bead is 0x34, with a range of 0x00 to 0xFF. |
| 0x56 | The Blue value for the first LED bead is 0x56, with a range of 0x00 to 0xFF. |
| 0x78 | The Lightness value for the first LED bead is 0x78, with a range of 0x00 to 0xFF. |

The same applies to the values for the other LED beads.

## LegLightControlSrv.srv

|         Type          |    Name    |       Description        |
| :-------------------: | :--------: | :----------------------: |
| bool | is_control | Take control |
| uint8 | target_leg_light | Target leg light |
| uint32[10] | light_rgbl_value | LED bead RGBL values |
| bool | success | Result returned |

**the value for take control：**

| is_control | Description |
| :--: | :---------: |
| false | Relinquish control |
| true | Take control |

**target leg liget range：**

| target_leg_light | Description |
| :--: | :---------: |
| 1 | Left leg light |
| 2 | Right leg light |

**Light bead RGBL value range:**

| light_rgbl_value | Description |
| :--: | :---------: |
| uint32[0] | RGBL value for the first LED bead |
| uint32[1] | RGBL value for the second LED bead |
| uint32[2] | RGBL value for the third LED bead |
| uint32[...] | Omitted |
| uint32[7] | RGBL value for the seventh LED bead |
| uint32[8] | RGBL value for the eighth LED bead |
| uint32[9] | RGBL value for the ninth LED bead |

**Assuming uint32[0] = 0x12345678, the specific meaning of the RGBL values 
for the first LED bead is:**

| uint32[0] | Description |
| :--: | :---------: |
| 0x12 | Placeholder value, no meaning |
| 0x34 | Red value for the first LED bead is 0x12, with a range of 0x00 to 0xFF |
| 0x56 | Green value for the second LED bead is 0x34, with a range of 0x00 to 0xFF |
| 0x78 | Blue value for the third LED bead is 0x56, with a range of 0x00 to 0xFF |

The same applies to the values for the other LED beads.



