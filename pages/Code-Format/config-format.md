# ROS2 param 模版

```{toctree}
:maxdepth: 1
:glob:
```

------

这是一个配置文件的内容模版。定义了 ROS2 中的参数，可以当启动节点且正确加载参数后。可以通过 ROS2 的参数服务器查看数据

- ros2 param list

```yaml
example_node:
  ros__parameters:
    value1: 1.0
    value2: 2.0
```

