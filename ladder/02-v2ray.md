# v2ray
> 暂且理解为 shadowsocks 增强版, 因为涵盖很多附加功能, 配置略复杂, 但推荐使用! 

> 尤其推荐它的路由功能, 有点类似 pac.js 自动代理; 可自定义策略, 根据 域名/IP/入口tag 等路由到不同出口, 实现相应的功能, 比如: 
1. 局域网或大陆地址 -> direct直连;
2. 被墙地址 -> proxy vps代理;
3. 广告地址 -> block 屏蔽;
4. 网易云音乐地址 -> unblockneteasemusic的http代理, 解锁灰名单;
5. 被公司局域网屏蔽的某些地址,比如视频网站 -> proxy aliyun代理;

- [官网](https://www.v2ray.com/)
- [github](https://github.com/v2ray)
- [新 V2Ray 白话文指南](https://guide.v2fly.org/#%E5%A3%B0%E6%98%8E)- [v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat/tree/master)

## 1. [安装](https://www.v2ray.com/chapter_00/install.html)
> 官网教程已经相当详细, 此处不再赘述.

- 服务端Linux一键安装/更新脚本
```bash
bash <(curl -L -s https://install.direct/go.sh)
```
- windows客户端 [v2rayN](https://github.com/2dust/v2rayN/releases)
- mac 客户端

[homebrew-v2ray](https://github.com/v2ray/homebrew-v2ray)

尝试了好几款mac客户端, 要么没有完全实现 `v2ray-core` 的功能(比如路由规则/DNS分流等), 要么就是稳定性太差. 所以直接使用
> 命令行 + [shuttle](https://github.com/fitztrev/shuttle/wiki)

## 2. 配置
当前热门的配置方式为: websocket + tls + web + CDN
> 简言之: 在vps上搭建反向代理web服务器, 通过 path 路由到 v2ray 的  websocket 服务
1. 给vps配置个域名, 例 `www.vps.com`
2. 给域名申请 TLS 证书 (例如 阿里云Symantec 免费版)
3. 在vps上搭建 `web` 服务器, 比如 `Nginx`, 增加证书相关配置, 使其支持tls
4. 配置v2ray服务端, 开启websocket服务, 监听: 127.0.0.1:12345
  ```
   {
      "port": 12345,
	  "listen":"127.0.0.1",
      "protocol": "vmess",
      "tag": "proxy-vmess-in",
      "settings": {
          "clients": [
              {
                  "id": "xxxxx",
                  "level": 1,
                  "alterId": 64,
                  "email": "xxxxxx"
              },
              ...
          ]
      },
      "streamSettings": {
          "network": "ws",
		    "wsSettings": {
		        "path": "/v2ray"
	        }
      }
  }
  ```
5. Nginx 配置反向代理, 将来自 `www.vps.com/v2ray` 的请求指向 `127.0.0.1:12345`
6. CDN
   //todo

7. 配置v2ray客户端
   
## 使用 cloudflare worker 搭建
[edgetunnel](https://github.com/zizifn/edgetunnel)
[edgetunnel cm优化版](https://github.com/cmliu/edgetunnel/)
[better-cloudflare-ip](https://github.com/badafans/better-cloudflare-ip/)

