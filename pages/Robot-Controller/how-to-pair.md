# 遥控手柄配对指南

```{toctree}
:maxdepth: 1
:glob:
```

------
该操作指南用于遥控器第一次配对机器人时的步骤指南。

## 配对步骤

### 连接终端

```shell
ssh root@192.168.55.1
```

调试线必须插入DBG口，并且数据线A面朝外。

1. 主控执行以下指令

    ```shell
    crsf-app -bind
    ```

    可以观察到返回：

    ```
    正在检查串口通讯状态...
    uart connect success
    正在进入配对模式...
    bind mode success
    ```

    请打开遥控器，左长按右侧按键进入`TOOLS -> ExpressLRS -> [Bind]`，手动搜索配对。
    ![controller1](../../../_static/controller1.png)

2. 遥控器开机后右边按键向左推进入界面后按键依次进入`Tools -> ExpressLRS -> bind`模式，进行配对接收机。
 ![controller2](../../../_static/controller2.JPEG)
 ![controller3](../../../_static/controller3.JPEG)

4. 配对完成返回`pair success`。
![controller4](../../../_static/controller4.PNG)

