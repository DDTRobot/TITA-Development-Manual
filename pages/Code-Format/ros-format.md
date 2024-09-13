# ROS2 程序结构

```{toctree}
:maxdepth: 1
:glob:
```

------

## 一、ROS 包组成

```bash
└── example_pkg
    ├── CMakeLists.txt
    ├── config
    │   └── param.yaml
    ├── include
    │   └── example_pkg
    │       ├── example_node.hpp
    │       └── user_function.hpp
    ├── launch
    │   └── example.launch.py
    ├── package.xml
    └── src
        ├── example_node.cpp
        ├── main.cpp
        └── user_function.cpp
```

- config 中存放的是本节点中包含的参数配置文件
- launch 中包含了启动本节点需要启动的必要 Node。如以相机为例，若要启动 vslam 则必须要同时启动相机节点。
- main.cpp 程序的唯一入口。只负责配置参数和实例化 ROS 节点。
- user_function.cpp 用户的所有逻辑实现的指代，用户的逻辑文件可能有很多。
- example_node.cpp 负责调用所有用户逻辑，所有 ROS 中的定义以及 ROS 的解析在这部分完成，将 ROS 数据转为非 ROS 数据类型传入到 user_function 中。

## 二、自定义消息

```bash
└── example_pkg_interfaces
    ├── CMakeLists.txt
    ├── action
    │   └── ActionFiles.action
    ├── msg
    │   └── MsgFiles.msg
    ├── package.xml
    └── srv
        └── ServeFiles.srv
```

在一些情况下会不可避免的使用自定义的消息，因此建议将所有包的自定义接口写在一个统一的仓库里。这样对于其他机器使用自定义接口时只需要编译一个包就可以了，而不是从每一个包中将其自定义的消息整理出来。
