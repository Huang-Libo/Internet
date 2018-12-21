# IPsec VPN 服务器一键安装脚本

## 简介

项目的仓库：https://github.com/hwdsl2/setup-ipsec-vpn  

本方案使用 Linux 脚本一键快速搭建自己的 IPsec VPN 服务器。支持 `IPsec/L2TP` 和 `Cisco IPsec` 协议，可用于 Ubuntu/Debian/CentOS 系统。你只需提供自己的 VPN 登录凭证，然后运行脚本自动完成安装。  

其中，以 Libreswan 作为 IPsec 服务器，以及 xl2tpd 作为 L2TP 提供者。  

## 服务端安装

如果对防火墙的配置不熟悉，安装前，先停止和禁用 iptables ：`systemctl stop iptables.service & systemctl disable iptables.service`    

#### CentOS

下载安装脚本：  

```bash
wget https://git.io/vpnsetup-centos -O vpnsetup-centos.sh
```

打开脚本，给 YOUR_IPSEC_PSK, YOUR_USERNAME 和 YOUR_PASSWORD 变量设置默认值(三个变量分别代表 ：IPsec预共享密钥、VPN用户名、VPN密码)。  

最后开始安装：  

```bash
sh vpnsetup-centos.sh
```

服务端安装官方文档：https://github.com/hwdsl2/setup-ipsec-vpn  

## VPN 模式及客户端配置

#### IPsec/XAuth (推荐使用)

> IPsec/XAuth 模式也称为 "Cisco IPsec"。该模式通常能够比 IPsec/L2TP 更高效地传输数据（较低的额外开销）。

 在 Android, iOS 和 OS X 上均受支持，无需安装额外的软件。Windows 用户可以使用免费的 [Shrew Soft](https://www.shrew.net/download/vpn) 客户端。  
 
如果你在使用 Windows 并且不想安装额外的软件，则可以用 `IPsec/L2TP` 模式。  

配置 IPsec/XAuth VPN 客户端的官方文档：https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/clients-xauth-zh.md  

#### IPsec/L2TP

`IPsec/L2TP` 效率没有 `IPsec/XAuth` 高，但是 `IPsec/L2TP` 在 Android, iOS, macOS 和 Windows 上均受支持，无需安装额外的软件。  

如果不需要使用 Windows 系统，还是建议采用 `IPsec/XAuth` 模式。  

配置 IPsec/L2TP VPN 客户端的官方文档：https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/clients-zh.md   

#### IKEv2
 
IKEv2配置比较复杂，若无特殊需求，不推荐使用。

## 使用命令行配置 Linux VPN 客户端

https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/clients-zh.md#使用命令行配置-linux-vpn-客户端

https://gist.github.com/psanford/42c550a1a6ad3cb70b13e4aaa94ddb1c

## 配置文件和用户管理

> 更改 IPsec PSK 需要重启服务，添加和删除用户不需要。

#### 更改 IPsec PSK（一般不用改）

所有的 VPN 用户将共享同一个 `IPsec PSK`（预共享密钥）。`IPsec PSK` 保存在文件 `/etc/ipsec.secrets` 中。如果要更换一个新的 PSK，可以编辑此文件（完成后必须重启服务）：

```
%any  %any  : PSK "你的IPsec预共享密钥"
```

重启服务：  

```
service ipsec restart
service xl2tpd restart
```

#### 给 IPsec/XAuth 模式添加用户

对于 IPsec/XAuth ("Cisco IPsec")，VPN 用户信息保存在文件 `/etc/ipsec.d/passwd`。该文件的格式如下：  

```
用户名1:密码1的加盐哈希值:xauth-psk
用户名2:密码2的加盐哈希值:xauth-psk
... ...
```

这个文件中的密码以加盐哈希值的形式保存。该步骤可以借助比如 openssl 工具来完成：

```bash
# 以下命令的输出为：密码1的加盐哈希值
# 将你的密码用 '单引号' 括起来
openssl passwd -1 '密码1'
```

#### 给 IPsec/L2TP 模式添加用户

IPsec/L2TP，VPN 用户信息保存在文件 /etc/ppp/chap-secrets。该文件的格式如下：  

```
"用户名1"  l2tpd  "密码1"  *
"用户名2"  l2tpd  "密码2"  *
... ...
```

#### 参考文档

管理 VPN 用户：https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/manage-users-zh.md  

## 故障排查

#### 服务端故障排查

首先，重启 VPN 服务器上的相关服务：

```
service ipsec restart
service xl2tpd restart
```

检查 Libreswan (IPsec) 和 xl2tpd 日志是否有错误：  

```bash
# CentOS & RHEL
grep pluto /var/log/secure
grep xl2tpd /var/log/messages

# Ubuntu & Debian
grep pluto /var/log/auth.log
grep xl2tpd /var/log/syslog
```

查看 IPsec VPN 服务器状态：  

```
ipsec status
ipsec verify
```

显示当前已建立的 VPN 连接：  

```
ipsec whack --trafficstatus
```

#### 客户端故障排查

故障排查：https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/clients-故障排除  

## 卸载 VPN

https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/uninstall-zh.md

## FAQ

#### VPN 可连上，但是没有网络：iptables 引发的问题

VPN 在服务器刚装好时就安装了，之后才安装的 ss。VPN 刚装好时，是可以正常使用的。  

之后，我又安装了 ss，但是 ss 服务起来后，客户端无法正常使用。经过一番折腾，发现和 iptables 有关。查看 iptables 状态：`systemctl status iptables.service`，停止和禁用 iptables ：`systemctl stop iptables.service & systemctl disable iptables.service`。

但是之后发现 VPN 出问题了，可以连上但是没有网络，怀疑和 iptables 有关。查看配置文件 `/etc/sysconfig/iptables`，果然看到了和 VPN 相关的设置。可参考[这里](https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/uninstall-zh.md#centosrhel-1)。打开 iptables，发现 VPN 就能正常使用了，看来安装 VPN 的时候，安装脚本往 iptables 里面写了很多相关规则。但是由于这个时候 ss 和 iptables 不能共存（ss 没有配置相关规则），所以，决定将 VPN 卸载重装。再次安装前，先关闭 iptables，避免脚本往里面写规则。  

分析：安装 VPN 时，iptables 是开启的，所以安装脚本把规则写入了 iptables 的配置文件中。如果想手动改回比较麻烦，卸载掉重装比较快。安装前，先停止和禁用 iptables。  

结果：卸载 VPN、关闭 iptables 后，重新安装 VPN，再次打开  iptables，VPN 就能正常使用了。ss也能正常使用，什么原理？？有时间得研究一下 iptables。

