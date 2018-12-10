# 1. SS 
境外服务器上安装
- [官网](http://shadowsocks.org/en/index.html)
- [Github](https://github.com/shadowsocks)
- [Feature Comparison across Different Versions](https://github.com/shadowsocks/shadowsocks/wiki/Feature-Comparison-across-Different-Versions)

| platform | github | abstract | 备注 |
| :-: | :-: | :-: | :-: |
| All | [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev) | libv版本: core | **☆☆☆☆☆** | 
| All | [shadowsocks](https://github.com/shadowsocks/shadowsocks/tree/master) | python版本: core
| Linux | [shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5) | core + UI, Linux + mac + windows 跨平台, mac和Windows两个平台需要根据源码自行编译
| Mac | [shadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG) | core + UI | 配置并启动后, 浏览器端可直接使用, 但 terminal 需要搭配 proxychains 使用
| Windows | [shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows) | core + UI
| Android | [shadowsocks-android](https://github.com/shadowsocks/shadowsocks-android) | core + UI | 配置并启动后可直接使用
| IOS | [superwingy] | core + UI | 配置并启动后可直接使用
| OpenWrt | core: [openwrt-shadowsocks](https://github.com/shadowsocks/openwrt-shadowsocks)<br>UI for config: [luci-app-shadowsocks](https://github.com/shadowsocks/luci-app-shadowsocks) | 路由器 | 可配置透明代理

- ss-redir
    >//todo
    
- ss-tunnel
    >//todo

* Optimize

  [Optimizing-Shadowsocks](https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks)

  [TCP-Fast-Open](https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open)

* Log

  `less /var/log/shadowsocks.log`

在路由器未配置透明代理或本机没有配置全局代理的情况下, 需要对各个客户端逐个配置代理:
(以下皆假设本地 sslocal 已经配置好, 监听1080端口)

## 1.1 浏览器代理
> sslocal 运行后, 浏览器并不会直接走socks5代理, 需要使用 [SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega) 插件进行代理. (sslocal 相当于实现了 socks5 协议的server端, SwitchyOmega 相当于实现了 socks5 的 client 端)

以下为配置方式:
![proxy模式](/images/switchyOmega_proxy.jpg)
![auto-proxy模式](/images/switchyOmega_auto.jpg)
>规则列表网址: https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt

## 1.2 Terminal 代理
> sslocal 运行后, 终端并不会直接走 socks5 代理, 需要使用cli工具 [proxychains](https://github.com/rofl0r/proxychains-ng) 进行终端代理. (作用等同于chrome插件 SwitchyOmega)
- 安装
```bash
# Linux
sudo apt install proxychains
# Mac
brew install proxychains-ng
```
- 配置
```bash
# Linux
vim /etc/proxychains.conf
# Mac
vim /usr/local/etc/proxychains.conf
```
在这个配置文件最下面有[ProxyList]这么一行，在这行下面添加上
```
socks5  127.0.0.1   1080
```
如果有别的比如 `socks4 127.0.0.1 9050`, 就把它给注释掉
- 使用

在原有命令前加上 `proxychains` , 比如:
```
proxychains git clone https://github.com/haad/proxychains.git
```

## 1.3 SSH 配置代理
创建配置文件 `~/.ssh/config`
```
Host <指定的要走代理的域名>
  ProxyCommand=nc -X 5 -x localhost:1080 %h %p
```

## 1.4 Git 配置代理
> git repo主要使用三种协议：git, http, ssh; 
### 1.4.1 对于http协议的git repo

```bash
# 走http/https代理
git config --global https.proxy 'http://127.0.0.1:1080'
git config --global https.proxy 'https://127.0.0.1:1080'

# 走socks5代理
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy

```

### 1.4.2 对于ssh协议的git repo
> 同1.3 SSH 配置代理

### 1.4.3 配置代理的scope
对于git全局用 `git config --global`

对于当前repo用 `git config --local`

参考：
- https://segmentfault.com/q/1010000000118837
- https://www.mikeheijmans.com/sysadmin/2014/08/12/proxy-ssh-over-socks/

## 1.5 Gradle 配置代理
创建 `gradle` 全局配置文件 `~/.gradle/gradle.properties`
输入以下内容
```bash
org.gradle.jvmargs=-DsocksProxyHost=127.0.0.1 -DsocksProxyPort=1080
```


[raspberrypi](https://www.jianshu.com/p/87f19de08877)

# 2. 加速

## 2.1 锐捷加速

[https://www.freehao123.com/vps-net-speeder-serverspeeder/](https://www.freehao123.com/vps-net-speeder-serverspeeder/) [https://www.91yun.org/serverspeeder91yun](https://www.91yun.org/serverspeeder91yun)

## 2.2 谷歌BBR加速\(✨\)

>Google开源TCP [BBR拥塞控制算法](https://github.com/google/bbr)（简称BBR），可以应用到常规的KVM和XEN架构的VPS、服务器中，用来提升服务器的速度。 [Ubuntu升级内核,开启BBR加速]() **需升级内核，五星推荐，实测效果非常明显（ping值虽没有明显改善，但下行速度提升相当明显）。** 

确定bbr已经成功开启
```bash
➜  ~ sysctl net.ipv4.tcp_available_congestion_control
net.ipv4.tcp_available_congestion_control = bbr cubic reno
➜  ~ lsmod | grep bbr
tcp_bbr                 6015  17
```
打开视频，自动切换为1080P，无压力 ![Paste\_Image.png](http://upload-images.jianshu.io/upload_images/1200965-814855105f202ab5.png?imageMogr2/auto-orient/strip|imageView2/2/w/720)

因新升级后的内核版本过高，锐捷加速不支持此内核。所以目前两种加速方式只能二选一 1.2

## 2.3 SS中继加速\(境内服务器上安装\)

中继加速（也叫中转，因为国内VPS效果最好所以一般都叫国内中转），是一种技术难度低，但是颇费钱的一种方法。而且要选好的服务器，加速效果才明显。原理如下:

> 本地终端\(sslocal\) &lt;==&gt; 境内VPS\(阿里云\) &lt;==&gt; 境外VPS\(ssserver\)&lt;==&gt;被墙的网站

HaProxy是其中的方法之一，使用方便，只支持TCP转. \(当然对iptables熟悉的, 建议直接用iptables的forward链进行转发\)

* 安装

  ```bash
  apt -y install haproxy
  ```

* 配置

  ```vim /etc/haproxy/haproxy.cfg``` 修改内容如下:
```
global
 
defaults
    log global
    mode    tcp
    option  dontlognull
        timeout connect 5000
        timeout client  50000
        timeout server  50000
 
frontend ss-in
    bind *:6666
    default_backend ss-out
 
backend ss-out
    server server1 233.233.233.233 maxconn 20480
```

其中6666换成你境外vps上搭建的ss的port, 233.233.233.233 替换成你ss的ip, 以上配置完成
- 启动
```
service haproxy start
```

- 设置为开机自启
```
systemctl enable haproxy
```
[参考文档](https://doub.io/ss-jc29/)


## 2.4 KCP加速
- 项目简介
    - [KCP github](https://github.com/skywind3000/kcp)
    - [kcptun github](https://github.com/xtaci/kcptun)

- server

    一键安装脚本
    ```bash
    wget https://github.com/kuoruan/shell-scripts/raw/master/kcptun/kcptun.sh
    chmod +x kcptun.sh
    # 运行脚本, 根据提示进行配置.
    ./kcptun.sh
    ```
    以上运行成功后会在终端输出client端的配置信息, 注意留存.

- client
    - Mac
        - cli方式
            
            1. 下载安装
            ```bash
            # https://github.com/xtaci/kcptun/releases 下载最新版kcptun
            wget https://github.com/xtaci/kcptun/releases/download/v20181114/kcptun-darwin-amd64-20181114.tar.gz
            # 解压
            tar xzvf kcptun-darwin-amd64-20181114.tar.gz
            cd kcptun-darwin-amd64-20181114 
            ```
            2. 准备配置文件 kcptun_client_config.json
            ```json
            {
                "localaddr": ":8989",
                "remoteaddr": "your_vps_ip:port",
                "key": "your_custom_key",
                "crypt": "aes-192",
                "mode": "fast2",
                "mtu": 1350,
                "sndwnd": 1024,
                "rcvwnd": 1024,
                "datashard": 10,
                "parityshard": 3,
                "dscp": 0,
                "nocomp": false,
                "quiet": false
            }
            ```
            3. 运行
            ```
            ./client_darwin_amd64 -c kcptun_client_config.json
            ```
            4. 修改sslocal的配置

            kcp运行成功后, 修改本地 `sslocal` 的配置文件, `server` 改成 `127.0.0.1`, `server_port` 同 kcptun_client_config 中的 `localaddr`. 最后重启 `sslocal`.
            ```json
            {
              "server":"127.0.0.1",
              "server_port":8989,
              "local_address":"127.0.0.1",
              "local_port":1080,
              "password":"your_password",
              "timeout":600,
              "method":"aes-256-cfb",
              "fast_open":true
            }
            ```
            
            5. 进阶使用

            使用 `launchd` 配置开机自启
            (据说 `Linux` 中的 `Systemd` 就是抄袭的 `launchd`)<br>
            ```
            # 进入 launchd 配置文件目录
            cd ~/Library/LaunchAgents
            # 新建并编辑配置文件(名字自己起, 也可以用vscode, xcode等其他编辑器编辑)
            vim com.jessewo.kcptun_client.plist
            ```
            配置文件内容入下:
            ```xml
            <?xml version="1.0" encoding="UTF-8"?>
            <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
            <plist version="1.0">
            <dict>
	            <key>KeepAlive</key>
	            <true/>
	            <key>Label</key>
	            <string>com.jessewo.kcptun_client</string>
	            <key>ProgramArguments</key>
	            <array>
	            	<string>/usr/local/bin/kcptun_client</string>
	            	<string>-c</string>
	            	<string>/etc/kcptun_client_config.json</string>
	            </array>
	            <key>StandardErrorPath</key>
	            <string>/Users/jessewo/Library/Logs/kcptun/kcptun_client.log</string>
	            <key>StandardOutPath</key>
	            <string>/Users/jessewo/Library/Logs/kcptun/kcptun_client.log</string>
	            <key>Debug</key>
	            <true/>
            </dict>
            </plist>
            ```
            字段解释
            - Label :Contains a unique string that identifies your daemon to launchd. (required) (任务的唯一标示)

            - ProgramArguments: Contains the arguments used to launch your daemon. (required) (命令行)

            - KeepAlive :This key specifies whether your daemon launches on-demand or must always be running. It is recommended that you design your daemon to be launched on-demand. (开机自启)
            
            参考文档:
            
            - [Apple官方文档](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html)<br>
            - [利用 Launchd 定制 Mac 启动任务](https://sspai.com/post/37258#01)
            
        - GUI方式
            
            下载安装[shadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG/releases)<br/>
            kcptun 以插件形式集成到了里面
    - Windows
        
        //todo
    - Android
        
        下载安装 shadowsocks 的 `kcptun` 插件.<br/>
        https://github.com/shadowsocks/kcptun-android <br/>
        输入配置, 修改端口号.
    
    - OpenWrt
        
        [luci-app-kcptun](https://github.com/kuoruan/luci-app-kcptun)

- 测速
fast.com