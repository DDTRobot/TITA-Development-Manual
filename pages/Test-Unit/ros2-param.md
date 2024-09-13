# ROS2 参数定义

```{toctree}
:maxdepth: 1
:glob:
```

------

​	ros 的参数，由参数服务器统一管理，可以通过 `ros2 param list` 来查看当前运行的功能包里包含多少参数。

```bash
root@docker-desktop:/# ros2 param list
/example_node:
  qos_overrides./parameter_events.publisher.depth
  qos_overrides./parameter_events.publisher.durability
  qos_overrides./parameter_events.publisher.history
  qos_overrides./parameter_events.publisher.reliability
  use_sim_time
  value1
  value2
```

​	而且也可以通过 `ros2 param set` 和 `get` 的方法改变和获取参数。在做一些需要在线调试的工作时，可以十分方便的改变程序中的参数变量。在 `rqt` 中也可以通过拖动滑窗的快速的对数值进行修改。
