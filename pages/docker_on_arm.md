# Docker 在 ARM安装
<!-- ```{toctree}
:maxdepth: 1
:glob:
```
------ -->

Ref：https://blog.csdn.net/hbhgyu/article/details/131745528

## 1.更新系统包&安装依赖项
首先确保系统环境最新的
```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

## 2.添加 Docker GPG密钥及源
- 官方源（速度比较慢）
```bash
1. curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
2. echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
3. sudo apt update
```
- 阿里云(强烈建议)
```bash
1. curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
2. echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
3. sudo apt update
```
## 3. 更新APT包索引
确保 APT从Docker 仓库安装，而不是从默认的Ubuntu仓库安装：
```bash
apt-cache policy docker-ce
```

## 4. 安装Docker
使用以下指令安装Docker：
```bash
sudo apt install docker-ce
```
## 5.添加当前用户到docker组
当前用户添加到`docker`组，以避免每次运行Docker时使用`sudo`：
```bash
sudo usermod -aG docker ${USER}
```

## 6.配置镜像仓库
```bash
sudo vim /etc/docker/daemon.json
```
将内容修改为：
```
{
    "registry-mirrors": [
        "https://docker.mirrors.ustc.edu.cn/"
    ]
}

```
## 7.切换到`iptables-legacy`
某些系统使用`nftables`作为默认`iptables`后端，这可能导致与Docker的兼容性问题。你可以尝试切换到`iptables-legacy`：
```bash
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
```
然后重新启动Docker服务：
```bash
sudo systemctl restart docker
```
## 8.查看Docker service状态
```bash
sudo systemctl status docker
```
如果服务状态为`active (running)`，则说明Docker安装成功。
如下：
```
 docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2025-05-26 08:17:43 UTC; 25s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 93199 (dockerd)
      Tasks: 13
     Memory: 25.6M
        CPU: 384ms
     CGroup: /system.slice/docker.service
             └─93199 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

May 26 08:17:43 tita dockerd[93199]: time="2025-05-26T08:17:43.029580417Z" level=info msg="[graphdriver] using prior storage driver: overlay2"
May 26 08:17:43 tita dockerd[93199]: time="2025-05-26T08:17:43.029899791Z" level=info msg="Loading containers: start."
May 26 08:17:43 tita dockerd[93199]: time="2025-05-26T08:17:43.033214594Z" level=warning msg="Could not load necessary modules for IPSEC rules: protocol not supported"
May 26 08:17:43 tita dockerd[93199]: time="2025-05-26T08:17:43.343225573Z" level=info msg="Loading containers: done."
May 26 08:17:43 tita dockerd[93199]: time="2025-05-26T08:17:43.362581504Z" level=info msg="Docker daemon" commit=01f442b containerd-snapshotter=false storage-driver=overlay2 version=28.1.1
May 26 08:17:43 tita dockerd[93199]: time="2025-05-26T08:17:43.362841131Z" level=info msg="Initializing buildkit"
May 26 08:17:43 tita dockerd[93199]: time="2025-05-26T08:17:43.407169339Z" level=info msg="Completed buildkit initialization"
May 26 08:17:43 tita dockerd[93199]: time="2025-05-26T08:17:43.419361273Z" level=info msg="Daemon has completed initialization"
May 26 08:17:43 tita dockerd[93199]: time="2025-05-26T08:17:43.419651429Z" level=info msg="API listen on /run/docker.sock"
May 26 08:17:43 tita systemd[1]: Started Docker Application Container Engine.

```
## 9.测试Docker
```bash
sudo docker run hello-world
```
## 常见问题
安装Docker常见的报错如下：
```bash
robot@tita:~/docker$ sudo systemctl restart docker
Job for docker.service failed because the control process exited with error code.
See "systemctl status docker.service" and "journalctl -xeu docker.service" for details.
```
```bash
sudo dockerd --debug
......
DEBU[2024-09-12T07:44:17.824103335Z] /usr/sbin/iptables, [--wait -t filter -N DOCKER-ISOLATION-STAGE-1] 
DEBU[2024-09-12T07:44:17.825489729Z] /usr/sbin/iptables, [--wait -t filter -n -L DOCKER-ISOLATION-STAGE-2] 
DEBU[2024-09-12T07:44:17.826938205Z] /usr/sbin/iptables, [--wait -t filter -N DOCKER-ISOLATION-STAGE-2] 
DEBU[2024-09-12T07:44:17.828281717Z] /usr/sbin/iptables, [--wait -t filter -C DOCKER-ISOLATION-STAGE-1 -j RETURN] 
DEBU[2024-09-12T07:44:17.829875351Z] /usr/sbin/iptables, [--wait -A DOCKER-ISOLATION-STAGE-1 -j RETURN] 
DEBU[2024-09-12T07:44:17.945520319Z] /usr/sbin/iptables, [--wait -t filter -F DOCKER-ISOLATION-STAGE-2] 
DEBU[2024-09-12T07:44:17.948470617Z] /usr/sbin/iptables, [--wait -t filter -X DOCKER-ISOLATION-STAGE-2] 
DEBU[2024-09-12T07:44:17.950528079Z] /usr/sbin/iptables, [--wait -t filter -F DOCKER-ISOLATION-STAGE-1] 
DEBU[2024-09-12T07:44:17.951960043Z] /usr/sbin/iptables, [--wait -t filter -X DOCKER-ISOLATION-STAGE-1] 
DEBU[2024-09-12T07:44:17.996985659Z] /usr/sbin/iptables, [--wait -t nat -D PREROUTING -m addrtype --dst-type LOCAL -j DOCKER] 
DEBU[2024-09-12T07:44:18.004361101Z] /usr/sbin/iptables, [--wait -t nat -D OUTPUT -m addrtype --dst-type LOCAL ! --dst 127.0.0.0/8 -j DOCKER] 
DEBU[2024-09-12T07:44:18.009870258Z] /usr/sbin/iptables, [--wait -t nat -D OUTPUT -m addrtype --dst-type LOCAL -j DOCKER] 
DEBU[2024-09-12T07:44:18.013839287Z] /usr/sbin/iptables, [--wait -t nat -D PREROUTING] 
DEBU[2024-09-12T07:44:18.014904771Z] /usr/sbin/iptables, [--wait -t nat -D OUTPUT] 
DEBU[2024-09-12T07:44:18.016268476Z] /usr/sbin/iptables, [--wait -t nat -F DOCKER] 
DEBU[2024-09-12T07:44:18.017408747Z] /usr/sbin/iptables, [--wait -t nat -X DOCKER] 
DEBU[2024-09-12T07:44:18.018885192Z] daemon configured with a 15 seconds minimum shutdown timeout 
DEBU[2024-09-12T07:44:18.018911914Z] start clean shutdown of all containers with a 15 seconds timeout... 
DEBU[2024-09-12T07:44:18.020172382Z] Cleaning up old mountid : start.             
DEBU[2024-09-12T07:44:18.020487947Z] Cleaning up old mountid : done.              
failed to start daemon: Error initializing network controller: error obtaining controller instance: failed to register "bridge" driver: unable to add return rule in DOCKER-ISOLATION-STAGE-1 chain:  (iptables failed: iptables --wait -A DOCKER-ISOLATION-STAGE-1 -j RETURN: iptables v1.8.7 (nf_tables):  RULE_APPEND failed (No such file or directory): rule in chain DOCKER-ISOLATION-STAGE-1
 (exit status 4))

```
```{note}
根据日志信息，Docker 服务启动失败是因为 `iptables` 配置出现了问题。错误信息指出了 `iptables` 在添加规则时的失败，具体是无法在 `DOCKER-ISOLATION-STAGE-1` 链中添加规则。
```
这种问题通常与`iptables`的配置或版本有关。以下是一些可能的解决方案：
### 1. 确认`iptabels`版本
确保你的`iptables`版本与系统和Docker版本兼容。你可以查询`iptables`版本：
```bash
sudo iptables --version
```
如果`iptables`版本较旧，考虑更新：
```bash
sudo apt update
sudo apt install iptables
```
### 2.切换到`iptables-legacy`
某些系统使用`nftables`作为默认`iptables`后端，这可能导致与Docker的兼容性问题。你可以尝试切换到`iptables-legacy`：
```bash
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
```
然后重新启动Docker服务：
```bash
sudo systemctl restart docker
```
### 3.清理旧的 `iptables`规则
Sometimes，清理了旧的`iptables`规则可以解决问题
```bash
sudo iptables -t filter -F
sudo iptables -t nat -F
sudo iptables -t mangle -F
sudo iptables -t raw -F
```
```{note}
注意：这会清空当前的 iptables 配置，可能影响系统的网络设置，请根据实际情况使用。
```
### 4.检查其他防火墙或网络工具
确保没有其他防火墙或网络工具干扰 `iptables` 配置。例如，`ufw（Uncomplicated Firewall）`可能会与 Docker 发生冲突。如果你使用 `ufw`，尝试禁用它：
```bash
sudo ufw disable
```
### 5.重新安装Docker
如果上述步骤无效，可以尝试重新安装docker
```bash
sudo apt remove --purge docker-ce docker-ce-cli containerd.io
sudo apt update
sudo apt install docker-ce
```
### 6.更新系统
确保你的操作系统是最新的，这样可以确保所有软件包和依赖项都是最新的：
```bash
sudo apt update
sudo apt upgrade
```
```{note}
执行这些步骤后，再次尝试启动 Docker 服务。如果问题依然存在，请提供更多细节给我司FAE，以便进一步排查。
```