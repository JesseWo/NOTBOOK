# shadowsocks
- [官网](http://shadowsocks.org/en/index.html)
- [Github](https://github.com/shadowsocks)
- [Feature Comparison across Different Versions](https://github.com/shadowsocks/shadowsocks/wiki/Feature-Comparison-across-Different-Versions)

shadowsocks 采用 `C/S` 架构, 以下列举了几种主要版本, 其中 `core` 主要包括 `sslocal` 和 `ssserver` 两个核心模块(shadowsocks-libev 还有其他模块), 顾名思义, sslocal 是 client 端, ssserver 是 server 端. 

所以在vps上部署时, 前两种版本二选一即可.

| platform | github | abstract | 备注 |
| :-: | :-: | :-: | :-: |
| All | [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev) | libv版本: core | **☆☆☆☆☆** | 
| All | [shadowsocks](https://github.com/shadowsocks/shadowsocks/tree/master) | python版本: core
| Linux | [shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5) | core + UI, Linux + mac + windows 跨平台, mac和Windows两个平台需要根据源码自行编译
| Mac | [shadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG) | core + UI | 配置并启动后, 浏览器端可直接使用, 但 terminal 需要搭配 proxychains 使用
| Windows | [shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows) | core + UI
| Android | [shadowsocks-android](https://github.com/shadowsocks/shadowsocks-android) | core + UI | 配置并启动后可直接使用
| IOS | [superwingy](https://apps.apple.com/cn/app/shadowing/id1194879940)<br/>BestWingy<br/>FirstWingy<br/>Shadowrocket | core + UI | 配置并启动后可直接使用
| OpenWrt | core: [openwrt-shadowsocks](https://github.com/shadowsocks/openwrt-shadowsocks)<br>UI for config: [luci-app-shadowsocks](https://github.com/shadowsocks/luci-app-shadowsocks) | 路由器 | 可配置透明代理

- ss-redir
    >//todo
    
- ss-tunnel
    >//todo

- 透明代理


* Optimize

  [Optimizing-Shadowsocks](https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks)

  [TCP-Fast-Open](https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open)

* Log

  `tail -n 20 -f /var/log/shadowsocks.log`

- 管理面板
  > 多用户管理或者商业用途
  - [shadowsocks-panel](https://github.com/sendya/shadowsocks-panel/tree/master)
  - [ss-panel](https://github.com/orvice/ss-panel/tree/master)

## 2 client 端
sslocal
