# ROS2 package xml 模版

```{toctree}
:maxdepth: 1
:glob:
```

------

ros2 中的 `package_xml` 是用来管理 ros2 的依赖关系的。可以使用 ros 的依赖管理工具 rosdep 对 ros 包的软件进行快速安装，而 rosdep 就是根据 xml 来判断需要安装哪些第三方软件的。

- `<buildtool_depend>`：指定用于构建包的工具（例如 `ament_cmake`）。
- `<build_depend>`：在构建时需要的包（例如 `rosidl_default_generators` 和 `std_msgs`）。
- `<exec_depend>`：在运行时需要的包（例如 `rclcpp` 和 `std_msgs`）。
- `<test_depend>`：在测试时需要的包（例如 `ament_lint_auto` 和 `ament_lint_common`）。

```xml
<?xml version="1.0"?>
<?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
<package format="3">
  <name>example_pkg</name>
  <version>0.0.0</version>
  <description>TODO: Package description</description>
  <maintainer email="user_mail@todo.todo">username</maintainer>
  <license>Apache License 2.0</license>

  <buildtool_depend>ament_cmake_auto</buildtool_depend>

  <depend>rclcpp</depend>
  <depend>sensor_msgs</depend>

  <test_depend>ament_lint_auto</test_depend>
  <test_depend>ament_cmake_clang_format</test_depend>
  <test_depend>ament_cmake_copyright</test_depend>
  <test_depend>ament_cmake_cppcheck</test_depend>
  <test_depend>ament_cmake_cpplint</test_depend>
  <test_depend>ament_cmake_lint_cmake</test_depend>
  <test_depend>ament_cmake_xmllint</test_depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>

```

