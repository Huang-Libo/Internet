# 用户自定义设置

## 用户自定义 PAC

GFW PAC + User rules for PAC = 最终 PAC 

获取最终 PAC：http://127.0.0.1:1089/proxy.pac

编辑用户 PAC 规则：https://adblockplus.org/en/filter-cheatsheet

加入代理：

```
||github.com^
```

如果前面加了 `@@`，就代表不走代理：

```
@@||baidu.com^
```

https://www.zybuluo.com/yiranphp/note/632963

https://fuyiyi.imdo.co/articles/2018/09/30/1538314978887.html

https://doubibackup.com/3we1qxzj-6.html

可以用这个网站做测试：

https://www.ip38.com/

## 插件

> 插件说明：https://shadowsocks.org/en/spec/Plugin.html

#### kcptun

[kcptun](https://github.com/xtaci/kcptun)：A Stable & Secure Tunnel Based On KCP with N:M Multiplexing

[kcptun-android](https://github.com/shadowsocks/kcptun-android)

#### simple-obfs

[simple-obfs-android](https://github.com/shadowsocks/simple-obfs-android)：simple-obfs plugin for shadowsocks-android.