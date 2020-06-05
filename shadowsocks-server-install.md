#  shadowsocks-libev 在服务端的安装、配置、运行 

shadowsocks-libev 项目的地址：https://github.com/shadowsocks/shadowsocks-libev  

##  安装 shadowsocks-libev

### 1. 使用 Snap 安装

[官方推荐](https://github.com/shadowsocks/shadowsocks-libev#quick-start)使用 [Snap](https://snapcraft.io/core) 来安装，适用于各类操作系统。

### 2. Ubuntu 中传统的安装方式

```bash
sudo apt update
sudo apt install -y shadowsocks-libev
```

### 3. CentOS 中传统的安装方式

从源码编译，参考：https://github.com/shadowsocks/shadowsocks-libev

### 4. 使用 pip 安装（不推荐）

网上提到的 pip 安装的是 [shadowsocks-python](https://github.com/shadowsocks/shadowsocks) 版本，应该是已停止维护（作者被喝%茶%🍵）了。

相关资料：  
https://pypi.org/project/shadowsocks/  
https://shadowsocks.org/en/download/servers.html  

## 配置 shadowsocks-libev

打开配置文件：

```bash
sudo vim /etc/shadowsocks-libev/config.json
```

然后写入（注意要替换密码）：

```
{
    "server":"0.0.0.0",
    "mode":"tcp_and_udp",
    "server_port":443,
    "local_port":1080,
    "password":"your-password",
    "timeout":60,
    "method":"xchacha20-ietf-poly1305"
}
```

## 管理 shadowsocks-libev

添加到服务：  

```bash
systemctl enable shadowsocks-libev
```

启动服务：  

```
systemctl start shadowsocks-libev
```

查看服务状态：  

```
systemctl status shadowsocks-libev
```

重启服务：  

```
systemctl restart shadowsocks-libev
```
