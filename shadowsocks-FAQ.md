# shadowsocks FAQ

## 服务端已部署好ss，状态检查正常，为何客户端连不上？

1. 检查 ip 是否能 ping 通。如果 ping 不通，可能是被墙了，也可能是 CPU 超负荷了导致的无响应，可以去管理后台看看 vps 的状态。
2. 查询端口是否开启：http://tool.chinaz.com/port
如果被墙了，端口就是关闭状态。
3. 请查看是否被服务端的防火墙阻止连接了。

`CentOS 7`：  

```bash
# 关闭防火墙
sudo service iptables stop
# 禁止防火墙开机启动
sudo systemctl stop iptables.service
```

如果熟悉防火墙配置也可以自行配置。  

**另外，有些云服务商的后台还有一套端口开关，需要用户去网站其后台打开需要使用的端口，比如青云。** 

## 未解疑问

看 YouTube 4k 视频，刚开始很流畅，但一两分钟后会导致服务器无法 ping 通，不知是运营商限速还是 vps 本身的问题。如果一直看 1080P 视频则无问题。是运营商限速导致的还是服务端的问题？