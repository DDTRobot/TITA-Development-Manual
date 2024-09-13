# ROS2 数据录制与播放

```{toctree}
:maxdepth: 1
:glob:
```

------

​	在 `ros` 的系统中为了能够记录某一个时段的数据，提供了 `ros2 bag record` 的工具用于记录各个节点发布的数据。而当需要再次使用时，就只需要通过 `ros2 bag play` 的方式将之前录制的数据重新播放。

- 使用 ros bag 的方法可以极大程度帮助测试。在不同的环境，通过 ros2 bag record 将功能包所需要的 topic 录制下来。之后再用播放的方式去 `ros2 bag play` 这样就可以保证环境变量的一致。及时的暴露出算法在不同场景的性能，且是完全可复现的（就不怕研发耍无赖了）
- ros bag 也是 ros 消息很好的载体，再录制完 ros bag 后可以将 bag 发送给其他人，来协助开发。

```bash
# 录制全部消息
ros2 bag record -a

# 录制指定的topic消息
ros2 bag record "topic1" "topic2"

# 播放指定的 bag 
ros2 bag play "bag"
```

### 一、bag 的测试流程

​	根据文档中节点的发布和订阅的描述，使用 ros bag play 录制文档中所有的 subscribed 的节点。运行仓库中的 launch 文件，启动测试节点。此时根据节点文档的描述，检查输出的 topic 状态，是否存在异常。

​	若存在异常状态，则可以通过 bag 定位到在什么样的工况下出现的异常，并将此部分的 bag 和现象反馈给研发。

```bash
# 播放录制的节点必须的信息
ros2 bag play "subscribed.bag"
# 启动测试节点的 launch 脚本
ros2 launch example_pkg example.launch.py
# 使用 rviz2 监看数据
# 使用 rqt 可视化变量分析曲线
```

