# VPS 

> [VPS](https://en.wikipedia.org/wiki/Virtual_private_server)（Virtual Private Server 虚拟专用服务器），是将一台服务器分割成多个虚拟专享服务器的服务。

## 说明

这次从 Ubuntu 换会 CentOS 系统了，下述都是讲的 CentOS 上的操作。（和 Ubuntu 略有差别而已）

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

其强大之处是可配置各种好用的插件，默认开启的有 `git` 插件。其他插件的配置可参看其 [Wiki](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins) 或 [插件代码仓库(每个插件都包含 Readme)](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins)（后者更实时） 。  

另外，还可以自行配置 theme，Wiki 里有[截图示例](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)。

oh-my-zsh 默认情况下每隔几周会检测一次升级。相关的配置在 `~/.zshrc` 中：

```bash
# 自动升级时是否询问
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

## 有趣的小工具

#### [magic-wormhole](https://github.com/warner/magic-wormhole)

> get things from one computer to another, safely.

###### 基本用法

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

###### 安装

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

## FAQ

玩一会就提示 `You have new mail.`，输入 `mail` 查看，提示 `command not found: mail`，需要安装 `mailx`：

```bash
yum install mailx
```

## 待研究的服务

[Caddy](https://caddyserver.com/)：Caddy is the HTTP/2 web server with automatic HTTPS.

