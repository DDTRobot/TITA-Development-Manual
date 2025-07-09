# Docker Installation on ARM
<!-- ```{toctree}
:maxdepth: 1
:glob:
```
------ -->

Ref：https://blog.csdn.net/hbhgyu/article/details/131745528

## 1.Update System Packages & Install Dependencies
First ensure the system environment is up-to-date
```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

## 2.Add Docker GPG Key and Source
- Official source (slow)
```bash
1. curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
2. echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
3. sudo apt update
```
- Aliyun (Recommended)
```bash
1. curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
2. echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
3. sudo apt update
```
## 3. Update APT Package Index
Ensure APT installs from Docker repository instead of default Ubuntu repository:
```bash
apt-cache policy docker-ce
```

## 4. Install Docker
Install Docker using:
```bash
sudo apt install docker-ce
```
## 5.Add Current User to Docker Group
Add current user to `docker` group to avoid using `sudo` for every Docker command:
```bash
sudo usermod -aG docker ${USER}
```

## 6.Configure Image Registry
```bash
sudo vim /etc/docker/daemon.json
```
Modify content to:
```
{
    "registry-mirrors": [
        "https://docker.mirrors.ustc.edu.cn/"
    ]
}

```
## 7.Switch to`iptables-legacy`
Some systems use `nftables` as default backend which may cause compatibility issues:
```bash
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
```
Then restart Docker service:
```bash
sudo systemctl restart docker
```
## 8.Check Docker Service Status
```bash
sudo systemctl status docker
```
If status shows `active (running)`, Docker is successfully installed:
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
## 9.Test Docker
```bash
sudo docker run hello-world
```
## Common Issues
Common Docker installation errors:
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
Based on the logs, Docker service failed to start due to `iptables` configuration issues. The error specifically indicates failure to add rules in the `DOCKER-ISOLATION-STAGE-1` chain.
```
This issue is typically related to `iptables` configuration or version. Possible solutions:
### 1. Confirm`iptabels`Version
Ensure your `iptables` version is compatible with the system and Docker:
```bash
sudo iptables --version
```
If outdated, update:
```bash
sudo apt update
sudo apt install iptables
```
### 2.Switch to `iptables-legacy`
Some systems use nftables as the default backend for iptables, which may cause compatibility issues with Docker. You can try switching to iptables-legacy:
```bash
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
```
Restart Docker service：
```bash
sudo systemctl restart docker
```
### 3.Clean Old `iptables` Rules
Clearing old rules may resolve the issue:
```bash
sudo iptables -t filter -F
sudo iptables -t nat -F
sudo iptables -t mangle -F
sudo iptables -t raw -F
```
```{note}
Warning: This will clear current iptables configuration and may affect network settings.
```
### 4.Check Other Firewalls or Network Tools
Ensure no other tools like `ufw` are interfering:
```bash
sudo ufw disable
```
### 5.Reinstall Docker
If previous steps fail:
```bash
sudo apt remove --purge docker-ce docker-ce-cli containerd.io
sudo apt update
sudo apt install docker-ce
```
### 6.Update System
Ensure OS is fully updated:
```bash
sudo apt update
sudo apt upgrade
```
```{note}
If issues persist after these steps, contact our FAE with detailed logs for further troubleshooting.
```