# 记录连接世界的历程

## vps

**翻**(和)**墙**(谐)，首先得租一个 [VPS](https://en.wikipedia.org/wiki/Virtual_private_server)（Virtual Private Server 虚拟专用服务器，是将一台服务器分割成多个虚拟专享服务器的服务）。  

推荐 [Vultr](https://www.vultr.com/?ref=6960892)，按小时计费，可随时部署和删除。最低价格为 \$5/月（偶尔做活动会出现 \$3.5 的。\$2.5 的只有 ipv6 网络所以不推荐）。可多人共用一台，非常划算。支付方式包括*信用卡、微信、支付宝*。  

比较快的 [Location](https://www.vultr.com/features/datacenter-locations/?ref=6960892) 有亚太地区的**日本、新加坡、首尔**，美国西海岸的**硅谷、洛杉矶、西雅图**。通常情况下亚太地区的 ping 值更低（亚太地区 30-150ms 左右，美国至少在 200ms 以上）。可以使用你的宽带对这些地区[测速](https://www.vultr.com/resources/faq/?ref=6960892#downloadspeedtests)。  

## 目录

- 翻墙方式一：**v2ray** (类似 shadowsocks，可配置为更隐蔽的代理服务器)
    - [v2ray](https://www.v2ray.com/) 的 vmess + websocket + tls 方案可伪装成 https 流量，安全性很高。（可选项一：使用 Ngnix，让伪装更真实。可选项二：使用 CDN。但使用国内 CDN 需要备案域名；而国外 CDN 会降低速度）
- 翻墙方式二：**shadowsocks**（适用于大多数情况）
    - [shadowsocks-libev 在服务端的安装、配置、运行](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-server-install.md)
    - [shadowsocks 客户端](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-client.md)
    - [shadowsocks FAQ](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-FAQ.md)
    - (可选项) [添加 PAC 规则，及插件介绍](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-custom-settings.md)
    - (可选项) [关于 shadowsocks 的更多资讯](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-read-more.md)
- [翻墙方式三：VPN（可全局翻墙）](https://github.com/Huang-Libo/Internet/blob/master/vpn.md)
- [服务器的基本设置、常用软件、日常维护](https://github.com/Huang-Libo/Internet/blob/master/server.md )

