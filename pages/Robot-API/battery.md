# Power Supply System

```{toctree}
:maxdepth: 1
:glob:
```

------

The API of the power supply system can only perform query actions on information data such as battery information

## Check the information of the left battery
**Function Overview：** Subscribe to the **Topic** for feedback on the left battery information.<br>
**Topic：** `system/batteries/left`<br>
**Msg Type：** `tita_system_msgs/msg/BatterieStates`<br>
**Code Example：** `ros2 topic echo /[namespace]/system/batteries/left`

## Check the information of the right battery
**Function Overview：** Subscribe to the **Topic** for feedback on the right battery information.<br>
**Topic：** `system/batteries/right`<br>
**Msg Type：** `tita_system_msgs/msg/BatterieStates`<br>
**Code Example：** `ros2 topic echo /[namespace]/system/batteries/right`<br>

## Check the information of the supercapacitor
**Function Overview：** Subscribe to the **Topic** for feedback on supercapacitor information.
**Topic：** `system/batteries/super`<br>
**Msg Type：** `tita_system_msgs/msg/BatterieStates`<br>
**Code Example：** `ros2 topic echo /[namespace]/system/batteries/super`

## Check the power supply statistics information
**Function Overview：** Subscribe to the **Topic** for feedback on power supply statistics information.<br>
**Topic：** `system/power_supply/info`<br>
**Msg Type：** `tita_system_msgs/msg/PowerSupplyInfo`<br>
**Code Example：** `ros2 topic echo /[namespace]/system/power_supply/info`
````{note}
Enable the power data upload feature by modifying the file /usr/share/power_bridges/conf/tita_power.toml, set record_battery_info=1 (#0 to disable, 1 to enable)
````