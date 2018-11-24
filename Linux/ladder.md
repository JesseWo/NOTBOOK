# 梯子
---
## 1. SS (境外服务器上安装)
- Install
    
    [Github地址](https://github.com/shadowsocks)
- Config
    ```
    vim /etc/shadowsocks.json
    ```

* **Optimize**

  [Optimizing-Shadowsocks](https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks)

  [TCP-Fast-Open](https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open)

* **Log**

  `less /var/log/shadowsocks.log`

[raspberrypi](https://www.jianshu.com/p/87f19de08877)

## 2. 加速

### 2.1 锐捷加速

[https://www.freehao123.com/vps-net-speeder-serverspeeder/](https://www.freehao123.com/vps-net-speeder-serverspeeder/) [https://www.91yun.org/serverspeeder91yun](https://www.91yun.org/serverspeeder91yun)

### 2.2 谷歌BBR加速\(✨\)

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

### 2.3 SS中继加速\(境内服务器上安装\)

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


### 2.4 KCP加速
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
            
            1. 下载安装
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
            # 进入 launchd 配置文件目录
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
            - Label :Contains a unique string that identifies your daemon to launchd. (required) (任务的唯一标示)

            - ProgramArguments: Contains the arguments used to launch your daemon. (required) (命令行)

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