# Locmotion Unit

```{toctree}
:maxdepth: 1
:glob:
```
------

​
Robot motion control management. It is mainly divided into the following 4 modules:

- **device**：Hardware bridge, currently handles the MCU commands sent by the remote controller, and reads the motor and IMU sensor information from the MCU．
- **libraries**：Third-party Library
- **locomotion_bringup**：Robot motion control bringup file.
- **locomotion_msgs**: Robot motion control message definition, currently only for debugging information.
- **tita_controllers**：Inherited from `controller_interface` in the ros2_control framework, it processes `hardware_interface` data and obtains control commands to be sent to `hardware_interface`.
- **tita_description**：Location for storing robot description files.
- **tita_webots_ros2**：Location for storing the robot simulation environment, hosted at `git@git.ddt.dev:rbt/alg/tita_webots_ros2.git`.

## Basic Information

| Installation method | Supported platform[s]    |
| ------------------- | ------------------------ |
| Source              | Jetpack 6.0 , ros-humble |

------

## Subscribed
1. `/${tita_ns}/command/manager/cmd_key` 
Topic type: `std_msgs/msg/String`
Robot state machine transition: The state machine includes: `transform_up`, `transform_down`, `balance`, `jump`, `idle`
    ``` bash
    ros2 topic pub -1 /${tita_ns}/command/manager/cmd_key std_msgs/msg/String "data: 'idle'"
    ```

2. `/${tita_ns}/command/manager/cmd_pose`    
Topic type: `geometry_msgs/msg/PoseStamped`
Robot head position and posture control commands, including adjusting height and yaw,`roll`, `pitch`
    ``` bash
    ros2 topic pub -1 /${tita_ns}/command/manager/cmd_pose geometry_msgs/msg/PoseStamped "{
        header: {
            stamp: {
                sec: 0, 
                nanosec: 0}, 
            frame_id: 'world'}, 
        pose: 
        {
            position: {x: 0.0, y: 0.0, z: 0.1}, 
            orientation: {x: 0.0, y: 0.0, z: 0.0, w: 1.0}
        }
        }"
    ```

3. `/${tita_ns}/command/manager/cmd_twist` 
Topic type: `geometry_msgs/msg/Twist`
Robot speed control commands, including `linear` and `angular`, with only `linear.x` and `angular.z` being effective.
    ``` bash
    ros2 topic pub -1 /${tita_ns}/command/manager/cmd_twist geometry_msgs/msg/Twist "{
        linear: {x: 0.1, y: 0.0, z: 0.0}, 
        angular: {x: 0.0, y: 0.0, z: 0.1}}"
    ```

## Published
1. `/${tita_ns}/joint_states`
Topic type: `sensor_msgs/msg/JointState`
Print robot joint information, including:`position`, `velocity`, `effort`

    ``` bash
    # ros2 topic echo /${tita_ns}/joint_states
    header:
    stamp:
        sec: 1728640435
        nanosec: 207354406
    frame_id: ''
    name:
    - joint_left_leg_1
    - joint_left_leg_2
    - joint_left_leg_3
    - joint_left_leg_4
    - joint_right_leg_1
    - joint_right_leg_2
    - joint_right_leg_3
    - joint_right_leg_4
    position:
    - 0.44081687927246094
    - 1.0672786235809326
    - -2.6032021045684814
    - 2.209383249282837
    - -0.5037123560905457
    - 1.1171343326568604
    - -2.625253915786743
    - 0.26672905683517456
    velocity:
    - -0.0
    - 0.010471980087459087
    - -0.0
    - 0.0
    - 0.0
    - -0.0
    - -0.0
    - -0.0
    effort:
    - -0.0
    - 0.030666524544358253
    - -0.0
    - -0.02499999850988388
    - 0.0
    - -0.0
    - -0.0
    - 0.016919462010264397
    ---
    ```

1. `/${tita_ns}/imu_sensor_broadcaster/imu`
Topic type: `sensor_msgs/msg/Imu`
Print robot IMU sensor information, include`orientation`, `angular_velocity`, `linear_acceleration`

    ``` bash
    # ros2 topic echo /${tita_ns}/imu_sensor_broadcaster/imu
    header:
    stamp:
        sec: 1728640659
        nanosec: 77332444
    frame_id: imu
    orientation:
    x: -0.004162624944001436
    y: 0.0013127117417752743
    z: -0.12123985588550568
    w: 0.9927361011505127
    orientation_covariance:
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    angular_velocity:
    x: -0.009841999970376492
    y: -0.004255999810993671
    z: -0.004788000136613846
    angular_velocity_covariance:
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    linear_acceleration:
    x: 0.0
    y: -0.08621344715356827
    z: 9.785225868225098
    linear_acceleration_covariance:
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    - 0.0
    ---
    ```
