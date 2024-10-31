# 遥控手柄配对指南

```{toctree}
:maxdepth: 1
:glob:
```

------
该操作指南用于遥控器第一次配对机器人时的步骤指南。

(在机器人中执行这个操作）
1. 使用`git clone` 将遥控器配对脚本克隆下来
`git clone http://git.ddt.dev:9281/wuyunzhou/crsf-app.git`
2. `cd crsf-app`
3. `chmod 777 install_ubuntu.sh`
4. `sudo ./install_ubuntu.sh`
5. 执行指令 `crsf-app -bind` ，可以观察到返回：   
```{bash}
root@apollo-nx:~# crsf-app -bind   
正在检查串口通讯状态...   
uart connect success   
正在进入配对模式...  
 bind mode success   
请打开遥控器,左长按右侧按键进入TOOLS->ExpressLRS->[Bind],手动搜索配对
```
![f9](../../_static/flash9.png)
6. 遥控器开机后 右边按键向左推进入界面后 按键依次进入Tools ->ExpressLRS-> bind模式，进行配对接收机.
 ![controller2](../../_static/controller2.JPEG)
 ![controller3](../../_static/controller3.JPEG)
7. 配对完成返回pair success
![controller4](../../_static/controller4.PNG)

