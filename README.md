# 记录连接世界的历程

## vps

翻墙首先得租一个 vps，推荐 [Vultr](https://www.vultr.com/?ref=6960892)，按小时计费，可随时部署和删除。最低价格为 \$3.5/月（\$2.5 的只有 ipv6 网络）。可多人共用一台，非常划算。支付方式包括*信用卡、微信、支付宝*。  

比较快的 [Location](https://www.vultr.com/features/datacenter-locations/?ref=6960892) 有亚太地区的日本、新加坡、首尔，美国西海岸的硅谷、洛杉矶、西雅图。通常情况下亚太地区的 ping 值更低（亚太地方 30-100ms 左右，美国至少在 200ms 以上）。可以使用你的宽带对这些地区[测速](https://www.vultr.com/resources/faq/?ref=6960892#downloadspeedtests)。  

## 目录

- 翻墙方式一：[v2ray](https://www.v2ray.com/)，其 vmess + websocket + tls 方案可伪装成 https 流量，安全性很高。（可选项一：使用 Ngnix，让伪装更真实。可选项二：使用 CDN，但国内 CDN 需要备案，国外 CDN 会降低速度）
- 翻墙方式二：shadowsocks（适用于大多数情况）
    - [shadowsocks-libev 在服务端的安装、配置、运行](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-server-install.md)
    - [安装 shadowsocks 客户端](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-client.md)
    - [shadowsocks FAQ](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-FAQ.md)
    - (可选项) [添加 PAC 规则，及插件介绍](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-custom-settings.md)
    - (可选项) [关于 shadowsocks 的更多资讯](https://github.com/Huang-Libo/Internet/blob/master/shadowsocks-read-more.md)
- [翻墙方式三：VPN（可全局翻墙）](https://github.com/Huang-Libo/Internet/blob/master/vpn.md)
- [服务器的基本设置、常用软件、日常维护](https://github.com/Huang-Libo/Internet/blob/master/server.md )
- [服务器的安全问题](https://github.com/Huang-Libo/Internet/blob/master/server-security.md)

