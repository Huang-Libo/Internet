# shadowsocks 客户端的配置

## 安装客户端

### Windows

[shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows/releases)

### Android

[shadowsocks-android](https://github.com/shadowsocks/shadowsocks-android/releases)

### macOS

1. GUI Client：[ShadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG/releases)   
2. Command-line Client：

```bash
brew install shadowsocks-libev
```

### iOS

shadowrocket（美区，\$2.99），Surge 3（美区，可免费下载，但有内购 \$49.99）

越狱设备可以使用 `Big Boss` ？

### Linux

1. GUI Client：[shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5) （ Cross-platform client for Windows/MacOS/Linux.）
2. Command-line Client：

```bash
sudo apt install shadowsocks-libev
```

### openwrt 系统的路由器

[openwrt-shadowsocks](https://github.com/shadowsocks/openwrt-shadowsocks)： shadowsocks-libev 在 OpenWrt 上的移植。 

### 一个非官方的实现：outline

#### 简介

是 Google 母公司 Alphabet 的一个孵化项目。

宗旨：Jigsaw is an incubator within Alphabet that uses technology to address geopolitical issues.

代码仓库：https://github.com/Jigsaw-Code
主页：https://getoutline.org

#### 服务端：[outline-server](https://github.com/Jigsaw-Code/outline-server)

开发工具：`Electron framework`    
平台：Window, Mac and Linux   
除了 `Outline Server`，还包含一个名为 `Outline Manager` 的管理后台。  

#### 客户端：[outline-client](https://github.com/Jigsaw-Code/outline-client)

开发工具： `Cordova`, `Electron framework`   
平台：Windows, Android / ChromeOS, iOS and macOS    