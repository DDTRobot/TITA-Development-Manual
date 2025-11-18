# 数据读取接口

```{toctree}
:maxdepth: 1
:glob:

```

------


### 电池状态查询接口
用于实时获取机器人电池的各项关键参数，支撑电量管理、低电量预警等功能。

```bash
  /**
     * @brief Get the current battery is connected.
     * @param index: the index of battery.
     * @return bool: if battery is connected, return true.
     */
  bool get_battery_is_connected(int index) const;
  /**
     * @brief Get the current battery voltage.
     * @param index: the index of battery.
     * @return float: current battery voltage in volts.
     */
  float get_battery_voltage(int index) const;
  /**
     * @brief Get the current battery temperature.
     * @param index: the index of battery.
     * @return float: current battery temperature in degrees Celsius.
     */
  float get_battery_temperature(int index) const;
  /**
     * @brief Get the current battery current.
     * @param index: the index of battery.
     * @return float: current battery current in amperes.
     */
  float get_battery_current(int index) const;
  /**
     * @brief Get the current battery percentage.
     * @param index: the index of battery.
     * @return float: current battery percentage in percent.
     */
  float get_battery_percentage(int index) const;
  /**
     * @brief Get the current battery cell voltage.
     * @param index: the index of battery.
     * @return std::vector<float>: current battery cell voltage in volts.
     */
  std::vector<float> get_battery_cell_voltage(int index) const;
```

### 机器人核心状态获取接口
用于获取机器人运动控制、姿态感知的关键数据，为运动规划、姿态调整提供基础，涵盖 IMU（惯性测量单元）、电机、关节三大模块：

```bash 
/**
     * @brief Get the current states update timeout.
     * @return bool: if current states not update, return true.
     */
  bool imu_data_timeout() const;
  /**
     * @brief Get the current states update timeout.
     * @return bool: if current states not update, return true.
     */
  bool motors_data_timeout() const;
  /**
     * @brief Get the current joint positions in joint space.
     * @return std::vector<double>: current joint positions in radians.
     */
  std::vector<double> get_joint_q() const;

  /**
     * @brief Get the current joint velocities in joint space.
     * @return std::vector<double>: current joint velocities in radians per second.
     */
  std::vector<double> get_joint_v() const;

  /**
     * @brief Get the current joint torques in joint space.
     * @return std::vector<double>: current joint torques in Newton meters.
     */
  std::vector<double> get_joint_t() const;

  /**
     * @brief Get the current joint status.
     * @note Joints status now is in bool value, true means the joint is online(TODO).
     * @return std::vector<uint16_t>: current joint status.
     */
  std::vector<uint16_t> get_joint_status() const;
  /**
     * @brief Get the current imu quaternion of mcu.
     * @note Quaternion sequence is x y z w.
     * @return std::array<double, 4>: current quaternion.
     */
  std::array<double, 4> get_imu_quaternion() const;  // x y z w

  /**
     * @brief Get the current imu acceleration of mcu.
     * @return std::array<double, 3>: current acceleration.
     */
  std::array<double, 3> get_imu_acceleration() const;

  /**
     * @brief Get the current imu angular velocity of mcu.
     * @return std::array<double, 3>: current angular velocity.
     */
  std::array<double, 3> get_imu_angular_velocity() const;

  /**
     * @brief Set the target joint feed-forward torques.
     * @param t the target joint feed-forward torques.
     * @return return true if the target is set successfully.
     */
  bool set_target_joint_t(const std::vector<double> & t);

  /**
     * @brief MIT control method. Set the target joint positions, velocities, kp, kd and feed-forward torques of the
     motors.
     * @param q the target joint positions in radians.
     * @param v the target joint velocities in radians per second.
     * @param kp the target joint proportional gains.
     * @param kd the target joint derivative gains.
     * @param t the target joint feed-forward torques.
     *
     * @return return true if the target is set successfully
     */
  bool set_target_joint_mit(
    const std::vector<double> & q, const std::vector<double> & v, const std::vector<double> & kp,
    const std::vector<double> & kd, const std::vector<double> & t);
    
```