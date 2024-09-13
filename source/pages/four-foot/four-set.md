# 四轮足模式配置使用指南

```{toctree}
:maxdepth: 1
:glob:
```

------
## 主机配置
1. 在确保硬件安装良好以及转接盒正确连接后。
2. 将USB线连接电脑和主机的DBG口，在电脑终端 `ssh root@192.168.55.1`。
3. 终端执行 `vim /usr/share/tita_bringup/params/default_param.yaml`。
4. 将该文件中6个motion_mode由0改为1。
5. 退出文件，并执行reboot。

## 从机配置
1. 将USB线连接电脑和从机的DBG口，在电脑终端 `ssh root@192.168.55.1`。
2. 终端执行 `vim /usr/share/tita_bringup/params/default_param.yaml`。
3. 将该文件中6个motion_mode由0改为2。
4. 退出文件，并执行reboot。
````{note}
普通 motion_mode : 0 
四轮足主机 motion_mode : 1 
四轮足从机 motion_mode : 2
````