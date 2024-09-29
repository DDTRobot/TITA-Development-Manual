# Lighting Effects

```{toctree}
:maxdepth: 1
:glob:
```

------

The API of the lighting effects can fully control 104 LED beads of the entire machine, allowing you to exchange colors, gradient effects, and so on.

## Front Light Effects Control
**Function Overview：** Control the Front Light Effects via Topic<br>
**Service：** `interaction_manager/light_control/head_light_control_srv`<br>
**Msg Type：**`tita_interaction_msgs/srv/HeadLightControlSrv`<br>
**Code Example：**<br>
Control：`ros2 service call /[namespace]/interaction_manager/light_control/head_light_control_srv tita_interaction_msgs/srv/HeadLightControlSrv "{head_light_control: {is_control: true, select_light_effect: 0, rgbl_value: [0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0x00000000]}}"`<br>
Value Range：<br>
**Bool is_control**， **Uin8_t select_light_effect**， **Uint32 rgbl_value[48]**<br>
**is_control** is set to **true** when control is required, and **false** when control is relinquished.<br>
**select_light_effect** = 0 , mean it is always on.<br>
In the array **Uin32_t rgbl[48]**, each element represents the red, green, blue, and brightness values of a single LED. For example, the color value of a certain LED is given as **0xfe00ff80U**. This value indicates that the **red** component is `254 (0xfeU)`, the **green** component is `0 (0x00U)`, the **blue** component is `255 (0xffU)`, and the brightness is `128 (0x80U)`.

## Rear Light Effects Control
**Function Overview：** Control the Rear Light Effects via Topic<br>
**Service：** `interaction_manager/light_control/tail_light_control_srv`<br>
**Msg Type：**`tita_interaction_msgs/srv/TailLightControlSrv`<br>
**Code Example：**<br>
Control：`ros2 service call /[namespace]/interaction_manager/light_control/tail_light_control_srv tita_interaction_msgs/srv/TailLightControlSrv "{tail_light_control: {is_control: true, select_light_effect: 0, rgbl_value: [0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00]}}"`<br>
Value Range：Bool is_control,，Uint8_t select_light_effect，Uin32_t rgbl_value[36]<br>

## Leg Light Effects Control
**Function Overview：** Control the leg light effects.<br>
**Service：** <br>
left leg`interaction_manager/light_control/left_leg_light_control_srv`<br>
right leg` interaction_manager/light_control/right_leg_light_control_srv`<br>
**Msg Type：**<br>
left leg`tita_interaction_msgs/srv/LegLightControlSrv `<br>
right leg`tita_interaction_msgs/srv/LegLightControlSrv`<br>
**Code Example：**<br>
Control：<br>
left leg `ros2 service call /[namespace]/interaction_manager/light_control/left_leg_light_control_srv tita_interaction_msgs/srv/LegLightControlSrv "{leg_light_control: {is_control: true, select_light_effect: 0, rgb_value: [0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff]}}"`<br>
right leg `ros2 service call /[namespace]/interaction_manager/light_control/right_leg_light_control_srv tita_interaction_msgs/srv/LegLightControlSrv "{leg_light_control: {is_control: true, select_light_effect: 0, rgb_value: [0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff]}}"`<br>
Value Range：uint8 select_leg_board，bool is_control，uint8 select_light_effect， uint32[10] rgb_value.<br>
```{note}
The basic control is the same as mentioned earlier. Set select_leg_board to 1 for the robot's left leg and to 2 for the right leg. 
The select_light_effect currently as a default value of 0, which represents a constant brightness.
Please note that the uint32_t rgb_value[10] only represents the red, green, and blue values, without brightness, as it is just a placeholder to fill the uint32_t. For example, a color value of 0xfe00ff80U for a certain LED bead indicates red: 254 (0xfeU), green: 0 (0x00U), blue: 255 (0xffU), and brightness: (default value is meaningless) for the overall presented color. For the LED beads on the legs, the higher the values of red, green, and blue you set, the brighter the corresponding LED bead will be, and vice versa, the lower the values, the dimmer the LED bead will be.
```

## Light Switch
**Function Overview：** You can control the power of the entire machine's light boards<br>
**Service：** `interaction_manager/light_control/light_power_switch_srv`<br>
**Msg Type：**`tita_interaction_msgs/srv/LightPowerSwitchSrv`<br>
**Code Example：**<br>
Control：`ros2 service call /[namespace]/interaction_manager/light_control/light_power_switch_srv tita_interaction_msgs/srv/LightPowerSwitchSrv "{light_power_switch: {is_head_light_power_on: true, is_tail_light_power_on: true, is_left_light_power_on: true, is_right_light_power_on: true}}"`<br>
Value Range：<br>
bool is_head_light_power_on<br>
bool is_tail_light_power_on<br>
bool is_left_light_power_on<br>
bool is_right_light_power_on<br>
```{note}
The default setting is true for all. Wherever you want to turn off the lights, set it to false.
```

## All machine lighting effect control
**Function Overview：** Control the state pointer of the entire machine's light board state machine.<br>
**Topic：** `interaction/light_control/light_fsm_control`<br>
**Msg Type：**`tita_interaction_msgs::msg::LightFsmControl`<br>
**Code Example：**<br>
Control：`ros2 topic pub /[namespace]/interaction/light_control/light_fsm_control tita_interaction_msgs/msg/LightFsmControl "{head_light_fsm: 1, tail_light_fsm: 1, left_leg_light_fsm: 1, right_leg_light_fsm: 1, head_fsm_lock: false, tail_fsm_lock: false, left_leg_fsm_lock: false, right_leg_fsm_lock: false}" -1`<br>
Inquiry：`ros2 topic echo /[namespace]/interaction/light_control/light_fsm_control tita_interaction_msgs/msg/LightFsmControl`<br>
Value Range：<br>
1. head_light_fsm，tail_light_fsm，left_leg_light_fsm，right_leg_fsm;value:0~255.<br>
2. head_fsm_lock,tail_fsm_lock,left_fsm_lock,right_fsm_lock; all bool<br>
```{note}
General inquiries are fine; control is used for debugging. 
The fsm_lock is used to lock the current state of the state machine, causing the robot to repeat the lighting effect for debugging purposes.
```