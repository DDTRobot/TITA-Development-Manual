# 灯效API

```{toctree}
:maxdepth: 1
:glob:
```

------

灯效API能完全控制整机104颗灯珠，能改变灯效的所有颜色和渐变等效果。<br>
腿部灯板控制指令要经过运控板的CANFD->CAN的转发，高频的控制会占用腿部电机CAN的通信带宽，所以限制了转发频率在200Hz(还需要进一步调整)，大约20帧灯效每秒。

## 前灯灯效控制
**功能概述：** 控制前灯灯效<br>
**Service：** `interaction_manager/light_control/head_light_control_srv`<br>
**Msg Type：**`tita_interaction_msgs/srv/HeadLightControlSrv`<br>
**命令示例：**<br>
控制：`ros2 service call /[namespace]/interaction_manager/light_control/head_light_control_srv tita_interaction_msgs/srv/HeadLightControlSrv "{head_light_control: {is_control: true, select_light_effect: 0, rgbl_value: [0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0x00000000]}}"`<br>
取值范围：<br>
**Bool is_control**， **Uin8_t select_light_effect**， **Uint32 rgbl_value[48]**<br>
**is_control**在需要控制时为**true**，放弃控制时为**false**。<br>
**select_light_effect**目前只取值0，为常亮。<br>
**Uin32_t rgbl[48]** 里，数组的每一个元素都表示一个灯珠的red,green,blue,brightness值，以某一个灯珠色彩：0xfe00ff80U为例，该值表示red:254(0xfeU), green:0(0x00U), blue:255(0xffU), brightness:128(0x80U)综合呈现的色彩。

## 尾灯灯效控制
**功能概述：** 控制尾灯灯效<br>
**Service：** `interaction_manager/light_control/tail_light_control_srv`<br>
**Msg Type：**`tita_interaction_msgs/srv/TailLightControlSrv`<br>
**命令示例：**<br>
控制：`ros2 service call /[namespace]/interaction_manager/light_control/tail_light_control_srv tita_interaction_msgs/srv/TailLightControlSrv "{tail_light_control: {is_control: true, select_light_effect: 0, rgbl_value: [0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00,0xff00ff00, 0xff00ff00, 0xff00ff00]}}"`<br>
取值范围：Bool is_control,，Uint8_t select_light_effect，Uin32_t rgbl_value[36]<br>

## 腿灯灯效控制
**功能概述：** 控制腿部灯效<br>
**Service：** <br>
左腿`interaction_manager/light_control/left_leg_light_control_srv`<br>
右腿` interaction_manager/light_control/right_leg_light_control_srv`<br>
**Msg Type：**<br>
左腿`tita_interaction_msgs/srv/LegLightControlSrv `<br>
右腿`tita_interaction_msgs/srv/LegLightControlSrv`<br>
**命令示例：**<br>
控制：<br>
左腿 `ros2 service call /[namespace]/interaction_manager/light_control/left_leg_light_control_srv tita_interaction_msgs/srv/LegLightControlSrv "{leg_light_control: {is_control: true, select_light_effect: 0, rgb_value: [0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff]}}"`<br>
右腿 `ros2 service call /[namespace]/interaction_manager/light_control/right_leg_light_control_srv tita_interaction_msgs/srv/LegLightControlSrv "{leg_light_control: {is_control: true, select_light_effect: 0, rgb_value: [0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff, 0xff00ffff, 0x00ffffff,0xffff00ff]}}"`<br>
取值范围：uint8 select_leg_board，bool is_control，uint8 select_light_effect， uint32[10] rgb_value.<br>
基本同上，select_leg_board = 1 (机器人左腿)，select_leg_board = 2 (机器人右腿) ，select_light_effect 目前值取0，为常亮 。<br>
```{note}
注意uint32_t 的rgb_value[10]只表示red,green,blue,没有brightness了，只是一个占位符填充uint32_t 以某一个灯珠色彩：0xfe00ff80U为例，该值表示red:254(0xfeU), green:0(0x00U), blue:255(0xffU), brightness:（缺省值无意义）综合呈现的色彩。 腿上的灯珠，填写的red,green,blue的值越大，这个对应的灯珠色彩越亮，反之灯珠越暗。
```

## 灯光开关
**功能概述：** 能控制整机的灯板开关<br>
**Service：** `interaction_manager/light_control/light_power_switch_srv`<br>
**Msg Type：**`tita_interaction_msgs/srv/LightPowerSwitchSrv`<br>
**命令示例：**<br>
控制：`ros2 service call /[namespace]/interaction_manager/light_control/light_power_switch_srv tita_interaction_msgs/srv/LightPowerSwitchSrv "{light_power_switch: {is_head_light_power_on: true, is_tail_light_power_on: true, is_left_light_power_on: true, is_right_light_power_on: true}}"`<br>
取值范围：<br>
bool is_head_light_power_on<br>
bool is_tail_light_power_on<br>
bool is_left_light_power_on<br>
bool is_right_light_power_on<br>
默认都是true 哪里想关掉，false哪里<br>

## 整机灯板状态机控制
**功能概述：** 能控制整机的灯板开关<br>
**Topic：** `interaction/light_control/light_fsm_control`<br>
**Msg Type：**`tita_interaction_msgs::msg::LightFsmControl`<br>
**命令示例：**<br>
控制：`ros2 topic pub /[namespace]/interaction/light_control/light_fsm_control tita_interaction_msgs/msg/LightFsmControl "{head_light_fsm: 1, tail_light_fsm: 1, left_leg_light_fsm: 1, right_leg_light_fsm: 1, head_fsm_lock: false, tail_fsm_lock: false, left_leg_fsm_lock: false, right_leg_fsm_lock: false}" -1`<br>
查询：`ros2 topic echo /[namespace]/interaction/light_control/light_fsm_control tita_interaction_msgs/msg/LightFsmControl`<br>
取值范围：<br>
1. head_light_fsm，tail_light_fsm，left_leg_light_fsm，right_leg_fsm取值均为0~255.<br>
2. head_fsm_lock,tail_fsm_lock,left_fsm_lock,right_fsm_lock均是bool型<br>
一般查询就行，控制用来debug的 fsm_lock用来锁住当前状态机指向的状态，使机器人重复灯效，debug用。<br>
