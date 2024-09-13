# ROS2 launch 启动管理器

```{toctree}
:maxdepth: 1
:glob:
```

------

`ros2 launch`是用于管理多个节点启动的工具。一般在 `launch` 文件中会配置节点的启动顺序，需要加载的参数或参数文件，以及需要remap 的 `topic` 的节点名称。由于这部分往往是使用 `python` 实现的，所以就算在编译过后，用户也可以在 `install` 目录中自行更改。

```python
import os
from ament_index_python.packages import get_package_share_directory
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    config = os.path.join(
        get_package_share_directory('example_pkg'),
        'config',
        'param.yaml'
    )

    return LaunchDescription([
        Node(
            package='example_pkg',
            executable='example_node',
            name='example_node',
            output='screen',
            parameters=[config]
        )
    ])

```

