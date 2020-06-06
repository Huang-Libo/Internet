# VPS 

> [VPS](https://en.wikipedia.org/wiki/Virtual_private_server)（Virtual Private Server 虚拟专用服务器），是将一台服务器分割成多个虚拟专享服务器的服务。

## 使用的操作系统

- CentOS 7 (without SELinux)
- Ubuntu 20.04

## 配置本机终端

### macOS

推荐 [iTerm2](https://www.iterm2.com/) (Mac only)。   

### Windows

[Cywin](https://www.cygwin.com/)？putty？  

听说微软自己搞了一个 Linux 环境子系统？

## 简化 vps 登录命令

### 方法一，在 `~/.zshrc` （更换为你使用的 shell 的配置文件）中添加变量：

```
export jp="root@IP"
```

- 将 *jp* 改为你的 vps 的 location，以便识别。  
- 将 *IP* 改为你的 vps 的 IP。  

设置好之后，刷新（或打开一个新终端）：

```
source ~/.zshrc
```

查看我们设置的变量是否生效：

```
echo $jp
```

如果设置成功了，就会打印相应内容；如果设置未生效，则输出为空。  

下次再登录时，就可以使用该变量：

```
ssh $jp
```

### 方法二，在 `iTerm2` 上配置 Profiles：

原理就是将用户名和密码（如果配置了 ssh key，则无需密码）写入到脚本中。按快捷键即可登录，不需要再输入登录命令。

## server 的认证方式

### 密码

第一次登陆时，用 root 的初始密码登录，登录后更改密码：

```bash
passwd
```

### 免密，在 server 的 authorized_keys 文件中配置 ssh key

先获取当前机器的公钥：

```bash
# mac 上可以用 pbcopy 这个命令
pbcopy < .ssh/id_rsa.pub
```

然后在 server 上的 `~/.ssh/authorized_keys` 文件中添加公钥。若目录和文件不存在则自行创建：  

```
mkdir .ssh
vim ~/.ssh/authorized_keys
```

将 `id_rsa.pub` 写入到 `~/.ssh/authorized_keys` 文件中。  

如果未生效，请配置 `.ssh` 目录和 `authorized_keys` 文件的权限：  

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

## 在 server 上配置 [oh-my-zsh](https://ohmyz.sh/)

> Oh My Zsh is an open source, community-driven framework for managing your zsh configuration.

先安装 `zsh`：

```bash
# CentOS
yum -y install zsh
# Ubuntu 20.04
apt -y install zsh
```

然后安装 oh-my-zsh：

```bash
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

其强大之处是可配置各种好用的插件，默认开启的有 `git` 插件。其他插件的配置可参看其 [Wiki](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins) 或 [插件代码仓库](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins)（每个插件都包含详细的文档） 。  

另外，还可以在 `~/.zshrc` 中自行配置 theme，Wiki 里有[截图示例](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)。vps 推荐使用 `ys` 主题。修改 `ZSH_THEME` 的值：  

```bash
ZSH_THEME="ys"
```

然后执行 `source .zshrc` 刷新：  

![ys theme](media/15908363956719.jpg)

此主题显示了用户名、主机名、当前目录，非常实用。  

oh-my-zsh 默认情况下每隔几周会检测一次升级。也可在 `~/.zshrc` 中配置：

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

## Ubuntu 使用 ifconfig

需要先安装 net-tools：  

```
sudo apt install net-tools
```

## 安装 Python3 和 pip3

### Ubuntu

Python3 一般都已有，pip3 需要自行安装：

```
sudo apt install -y python3-pip
```

### CentOS 

```
sudo yum -y update
yum install python3
```

如果，提示找不到 python3，可以先搜索：  

```
yum search python3
```

发现有很多结果，找到一个包名叫 `python36.x86_64` 的包，安装：

```
yum -y install python36
```

python3 自带 `pip3`，无需再安装。  

## magic-wormhole

> [magic-wormhole](https://github.com/warner/magic-wormhole): get things from one computer to another, safely.

### magic-wormhole 基本用法

发送方：

```bash
# 会生成一个 Wormhole code，需要发送给接收方。
wormhole send README.md
```

接收方：  

```bash
wormhole receive
```

更多资料请看详细的[文档](https://magic-wormhole.readthedocs.io/en/latest/)。  

### macOS 安装 magic-wormhole

```bash
# macOS 上需要通过 `xcode-select --install` 来获取 gcc
brew install magic-wormhole
```

### Ubuntu 安装 magic-wormhole

```bash
# Ubuntu
sudo apt -y install magic-wormhole
```

### CentOS 安装 magic-wormhole

使用 yum 安装（如果 repo 中没有，则可改用 pip3 安装，或者添加 Fedora 的 repo？）：

```bash
# CentOS
sudo yum -y install magic-wormhole
```

（使用 `pip3` 安装如果报错，可能需要通过 yum 安装 `python3-devel`）：

```bash 
yum search python3 | grep devel
# 看到了 python3-devel.x86_64, 安装它
yum -y install python3-devel
```

使用 `pip3` 安装：  

```bash 
# 为所有用户安装
sudo pip3 install magic-wormhole
# 也可以只给当前用户安装
pip3 install --user magic-wormhole
```

如果使用 wormhole 时编码（ASCII）报错：

```
RuntimeError: Click will abort further execution because Python 3 was configured to use ASCII as encoding for the environment. Consult https://click.palletsprojects.com/python3/ for mitigation steps.
```

解决方法，设置编码方式（参考 [stackoverflow](https://stackoverflow.com/questions/36651680/click-will-abort-further-execution-because-python-3-was-configured-to-use-ascii)）：

```
export LC_ALL=en_US.utf-8
export LANG=en_US.utf-8
```

## Gogs

> 低配置 vps 首选的 git 服务托管。

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
# 筛选结果
timedatectl list-timezones | grep Asia/Shanghai
```

将硬件时钟调整为与本地时钟一致, 0 为设置为 UTC 时间：  


```bash
# 不要用于 vps，仅用于设置本地服务器
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

### CentOS 添加 EPEL

[EPEL（Extra Packages for Enterprise Linux）](https://fedoraproject.org/wiki/EPEL)，是 Fedora 项目组推出的软件包。包含许多优质软件。  

安装 EPEL：  

```
yum install -y epel-release
```

### CentOS 报错：Failed to set locale, defaulting to C

输入 `locale`，打印：

```
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
LANG=en_US.UTF-8
LC_CTYPE=UTF-8
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
...
```

解决方式：

```bash
echo "export LC_ALL=en_US.UTF-8"  >>  /etc/profile
echo "export LC_CTYPE=en_US.UTF-8"  >>  /etc/profile
```

再重新登录即可。

### mail

玩一会就提示 `You have new mail.`，输入 `mail` 查看，提示 `command not found: mail`，需要安装 `mailx`：

```bash
yum install mailx
```

## 待研究的服务

[Caddy](https://caddyserver.com/)：Caddy is the HTTP/2 web server with automatic HTTPS.

