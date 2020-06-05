# [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev) 在服务端的安装、配置、运行 

##  安装 shadowsocks-libev

### Ubuntu

```bash
sudo apt update
sudo apt install -y shadowsocks-libev
```

### CentOS

从源码编译，参考：https://github.com/shadowsocks/shadowsocks-libev

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

```bash
# 将 shadowsocks-libev 添加到服务
systemctl enable shadowsocks-libev
# 启动 shadowsocks-libev 服务
systemctl start shadowsocks-libev
# 查看 shadowsocks-libev 的状态
systemctl status shadowsocks-libev
# 重启 shadowsocks-libev 服务
systemctl restart shadowsocks-libev
```
