# Sensor Status Information

```{toctree}
:maxdepth: 1
:glob:
```

------

View the status of all sensors, and provide feedback of all sensors on any abnormalities, uninitialized conditions, and so on.

------

**Topic：** `system/sensor_status`<br>
**Msg Type：** `tita_system_msgs::msg::SensorStatus`<br>
**Code Example：** `ros2 topic echo /[namespace]/system/sensor_status`<br>
### Field Description
- `header`：Standard metadata for higher-level data types with timestamps. This field is used to convey timestamp and coordinate frame information.<br>
- `infrared_status`：Status of the Infrared Sensor.<br>
- `ultrasonic_status`：Status of the Ultrasonic Sensor.<br>
- `camera_status`：Status of the Camera.<br>
- `left_motor_status`：Status of the left motors. This is a list of the status of each motor in the left motor group.<br>
- `right_motor_status`：Status of the right motors. This is a list of the status of each motor in the right motor group.<br>
- `temperature_humidity_status`：Status of the Temperature and Humidity Sensors.<br>
- `controller_status`：Status of the Controller.<br>
- `locomotion_status`：Status of the Motion System.
### Status Code
The status field in the message uses the following status codes:<br>
- `UNINITIALIZED = 0`：Sensor or system is uninitialized.<br>
- `OK = 1`：Sensor or system is functioning normally.<br>
- `ERROR = 2`：Sensor or system has encountered an error.<br>
- `OFFLINE = 3`：Sensor or system is offline.<br>
`locomotion_status`Fields use different status codes.<br>
- `DIE = 0x00`：The motion system has stopped.<br>
- `INIT = 0x01`：The motion system is initializing.<br>
- `TRANSFORM_UP = 0x02`：The motion system is transforming upwards.<br>
- `STAND = 0x03`：The motion system is standing.<br>
- `TRANSFORM_DOWN = 0x04`：The motion system is transforming downwards.<br>
- `CRASH = 0x05`：The motion system has crashed.<br>
- `SUSPENDING = 0x06`：The motion system is pausing.<br>
- `JUMP = 0x07`：The motion system is jumping.<br>
- `UNINITIALIZED_STATUS = 0x08`：The motion system is uninitialized.<br>