# VPS 

> [VPS](https://en.wikipedia.org/wiki/Virtual_private_server)（Virtual Private Server 虚拟专用服务器），是将一台服务器分割成多个虚拟专享服务器的服务。

## 操作系统：CentOS7

这次从 Ubuntu 换回 CentOS 系统了，下述都是讲的 CentOS 上的操作。（和 Ubuntu 略有差别而已）

## 配置本机终端

#### macOS

推荐 [iTerm2](https://www.iterm2.com/) (Mac only)。   

特性：https://www.iterm2.com/features.html  

#### Windows

putty？[Cywin](https://www.cygwin.com/)？  
听说微软自己搞了一个 Linux 环境子系统？

## 登录 server

#### 常规操作

第一次登陆时，用 root 的初始密码登录，登录后更改密码：

```bash
passwd
```

#### 另一种登录方式之1：  

可以在 server 上设置 ssh key，实现免密登录。

先获取当前机器的公钥：

```bash
# mac 上可以用 pbcopy 这个命令
pbcopy < .ssh/id_rsa.pub
```

然后在 server 上的 ` ~/.ssh/authorized_keys` 文件中添加公钥。（若目录和文件不存在则自行创建。）  

如果未生效，请配置 `.ssh` 目录和 `authorized_keys` 文件的权限：  

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

#### 另一种登录方式之2： 

在 `iTerm2` 上配置 Profiles 后可以使用快捷键登录。

## 在 server 上配置 [oh-my-zsh](https://ohmyz.sh/)

> Oh My Zsh is an open source, community-driven framework for managing your zsh configuration.

先安装 `zsh`：

```bash
# CentOS
yum -y install zsh
```

然后安装 oh-my-zsh：

```bash
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

其强大之处是可配置各种好用的插件，默认开启的有 `git` 插件。其他插件的配置可参看其 [Wiki](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins) 或 [插件代码仓库](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins)（每个插件都包含详细的 Readme） 。  

另外，还可以自行配置 theme，Wiki 里有[截图示例](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)。

oh-my-zsh 默认情况下每隔几周会检测一次升级。相关的配置在 `~/.zshrc` 中：

```bash
# 检测到新版本时，安装前是否询问用户
DISABLE_UPDATE_PROMPT=true
# 是否禁止自动升级
DISABLE_AUTO_UPDATE=true
```

如果想立即升级，可直接运行：

```bash
upgrade_oh_my_zsh
```

卸载：

```bash
uninstall_oh_my_zsh
```

## 翻墙工具

> vps 最重要的功能就是翻墙啦，所以有必要单独建个仓库来讨论。

shadowsocks，vpn，请查看 https://github.com/Huang-Libo/Internet 。

## 安装 Python3 和 pip3

```
sudo yum -y update
yum install python3
```

如果，提示找不到 python3，可以先搜索：  

```
yum search python3
```

发现有很多结果，找到一个包名叫 `python36.x86_64` 的包。

```
yum install python36
```

`pip3` 可以用上述方式安装，也使用下面[这种](https://pip.readthedocs.io/en/stable/installing/)方式：  



```bash
curl https://bootstrap.pypa.io/get-pip.py -「」 get-pip.py
python3 get-pip.py
```

## Gogs

> vps 上首选的 git 服务托管。

## [magic-wormhole](https://github.com/warner/magic-wormhole)

> get things from one computer to another, safely.

#### 基本用法

（也可参看详细的[文档](https://magic-wormhole.readthedocs.io/en/latest/)）： 

发送方：

```bash
# 会生成一个 Wormhole code，需要发送给接收方。
wormhole send README.md
```

接收方：  

```bash
wormhole receive
```

#### 安装

macOS

```bash
# macOS 上需要通过 `xcode-select --install` 来获取 gcc
brew install magic-wormhole
```

Linux

```bash
# Ubuntu
sudo apt install magic-wormhole
# CentOS（如果 repo 中没有，则可使用 pip3 安装）
sudo yum install magic-wormhole
```

说明：或者使用 `pip3` 安装（如果报错，可能需要通过 yum 安装 `python36-devel`，或参考[文档](https://magic-wormhole.readthedocs.io/en/latest/welcome.html#installation)）：

```bash 
# 为所有用户安装
sudo pip3 install magic-wormhole
# 也可以只给当前用户安装
pip3 install --user magic-wormhole
```

## 设置时区

查看当前日期、时区：

```bash
date
```

查看时区详细信息：  

```bash
timedatectl status
```

列出所有时区：  


```bash
# 结果会比较多
timedatectl list-timezones
# 筛选亚洲的结果
timedatectl list-timezones | grep Asia
```

将硬件时钟调整为与本地时钟一致, 0 为设置为 UTC 时间：  


```bash
timedatectl set-local-rtc 1
```

将系统时区设置为上海：  


```bash
timedatectl set-timezone Asia/Shanghai
```

**另一种方式**：不考虑各个发行版的差异化, 从更底层出发的话, 修改时间时区比想象中要简单，


```bash
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

参考资料：https://www.cnblogs.com/zhangeamon/p/5500744.html

## 添加有 sudo 权限的用户

可以先查看当前的`用户`信息和`用户组`信息：  

```bash
# 查看用户信息
vim /etc/passwd
#查看用户组信息
vim /etc/group
```

添加用户：  

```bash
# 添加用户
adduser username
# 给用户设置密码
passwd username
# 将用户添加到 wheel 用户组（对应 Ubuntu 上的 sudo 用户组）
usermod -aG wheel username
```

这样该用户就有 sudo 权限了。

## FAQ

玩一会就提示 `You have new mail.`，输入 `mail` 查看，提示 `command not found: mail`，需要安装 `mailx`：

```bash
yum install mailx
```

## 待研究的服务

[Caddy](https://caddyserver.com/)：Caddy is the HTTP/2 web server with automatic HTTPS.
