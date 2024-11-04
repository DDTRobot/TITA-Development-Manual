# RGB light effect controller

```{toctree}
:maxdepth: 1
:glob:
```
------
## Description
RThe RGB lighting controller is used to control all visible RGB lights on the entire machine, including the front light strip, rear light strip, and left/right leg lights of the TITA robot. It can achieve any color for any part of any light bead.

Since this interface uses custom messages, a detailed explanation is provided for this interface.

The front light strip consists of 48 RGB light beads. Each light bead is controlled by four dimensions: red, green, blue, and brightness. Therefore, each light bead can be controlled by data of the `uint32_t` type, with each dimension occupying 8 bits. The entire light strip can be controlled by an array of `uint32_t` type data containing 48 elements.

The rear light strip consists of 36 RGB light beads. Each light bead is controlled by four dimensions: red, green, blue, and brightness. Therefore, each light bead can be controlled by data of the `uint32_t` type, with each dimension occupying 8 bits. The entire light strip can be controlled by an array of `uint32_t` type data containing 36 elements.

The left leg/right leg light strips each consist of 10 RGB light beads. Each light bead is controlled by three dimensions: red, green, and blue. Therefore, each light bead can be controlled by data of the `uint32_t` type, with each dimension occupying 8 bits, and the remaining eight bits are meaningless. The entire light strip can be controlled by an array of `uint32_t` type data containing 10 elements. The left leg and right leg need to be controlled separately.

For example：
```
uint32_t head_rgb_light[48];
uint32_t tail_rgb_light[36];
uint32_t left_leg_rgb_light[10];
uint32_t right_leg_rgb_light[10];

head_rgb_light[0] = 0x12345678U;
tail_rgb_light[0] = 0x12345678U;
left_leg_rgb_light[0] = 0x12345678U;
right_leg_rgb_light[0] = 0x12345678U;

In this case, the first light bead of the front and rear light strips is set to `0x12345678U`. 
This means that the red value for the first light beads of the front and rear lights is `0x12U (18)`, the green value is `0x34U (52)`, the blue value is `0x56U (86)`, and the brightness value is `0x78U (120)`. 
The specific lighting effect is the result of the above values mixed together.


The first light bead of the left/right leg light strips is set to `0x12345678U`. T
his means that the red value for the first light bead of the left/right leg light strips is `0x12U (18)`, the green value is `0x34U (52)`, and the blue value is `0x56U (86)`. The `0x78U` value is not used and thus has no significance. 
The specific lighting effect is the result of the above values mixed together.
```

## Preparation

Run RGB light controller：
```
ros2 run rgb_light_controller rgb_light_controller_node 
or
ros2 launch rgb_light_controller rgb_light_controller_node.launch.py
```

## Usage
The lighting effect controller provides control interfaces in the form of services, and users have two methods to implement control:

**The first method involves directly invoking a debugging command to achieve one-time control：**
```
if control front light：
ros2 service call /system/light_control/head_light_control_srv tita_system_interfaces/srv/HeadLightControlSrv "{is_control: true, light_rgbl_value: [0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00]}"

if control rear light：
ros2 service call /system/light_control/tail_light_control_srv tita_system_interfaces/srv/TailLightControlSrv "{is_control: true, light_rgbl_value: [0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00,0xff00ff00]}" 

if control left/right leg light：
ros2 service call /system/light_control/leg_light_control_srv tita_system_interfaces/srv/LegLightControlSrv "{is_control: false, target_leg_light: 1, light_rgbl_value: [0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00]}"
target_leg_light is 1:left leg，2: right leg

Abandon control by setting `is_control` to `false`.
```
**The second approach involves constructing a Client within the program to send requests to a Service, achieving more efficient and flexible control.**

Please refrain from sending requests to the leg light strips at excessively high frequencies, as doing so may interfere with the communication of the leg motors.

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------


