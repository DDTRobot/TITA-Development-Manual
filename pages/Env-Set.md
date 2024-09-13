# 环境配置
----
本章节讲述如何配置二次开发编译环境

- 用Debug数据线插入机器前端DBG口后连接电脑
- 接线完成后打开命令终端，输入`ssh root@192.168.55.1`进入；
- 通过命令行配置或通过上位机（可在说明书上了解）配置WIFI连接情况；
- WIFI连接成功后，使用`docker pull`指令将Ubuntu docker下载；
`docker pullregistry.cn-hangzhou.aliyuncs.com/ddt_robot/nvidia-ubuntu`
- 下载完成后进行环境的配置，可打开`/lib/systemd/system/tita-vision.service`和`/lib/systemd/system/tita-bringup.service`这两个配置文件，修改两处变量`Environment="ROS_LOCALHOST_ONLY=0"`；
- 配置好环境后Restart docker即可/将自己开发的ROS2代码放进docker中编译。
