# ROS2 CMake 模版

```{toctree}
:maxdepth: 1
:glob:
```

------

这是一个 `CMakeLists.txt` 的模板，其中需要注意的有以下几点。

- 程序执行的入口 main.cpp。其中包含了调用参数文件和使用`MultiThreadedExecutor` 方法，使内部的订阅使用多线程的模式。

- `${PROJECT_NAME}_lib` 中包含了用户的 cpp 文件和一个 ROS node 的 cpp 文件。

  - 用户的 cpp 文件：用于实现程序的逻辑，不包含任何的 ROS 相关库。
  - ROS node 文件：定义所有 ROS 的相关组件，调用用户的 cpp 程序接口。

  这样做可以极大程序的将 ROS 的程序与用户的逻辑程序分开，因为在一些场景中是不适合使用 ROS 的，这样的结构可以将程序的逻辑部分做最大程度的复用。

```cmake
cmake_minimum_required(VERSION 3.8)
project(example_pkg)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()
set(CMAKE_CXX_FLAGS "-std=c++17 -Wall -O3")

# find dependencies
find_package(ament_cmake_auto REQUIRED)
ament_auto_find_build_dependencies()

include_directories(include)

ament_auto_add_library(${PROJECT_NAME}_lib SHARED
    src/user_function.cpp
    src/example_node.cpp
)

ament_auto_add_executable(example_node
    src/main.cpp
)

install(DIRECTORY launch DESTINATION share/${PROJECT_NAME})
install(DIRECTORY config DESTINATION share/${PROJECT_NAME})

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_auto_package()

```

