# Client端配置代理
>在路由器未配置透明代理或本机没有配置全局代理的情况下, 需要对各个客户端逐个配置代理:
(以下皆假设本地 sslocal 已经配置好, 监听1080端口)

## 1. 浏览器代理
> sslocal 运行后, 浏览器并不会直接走socks5代理, 需要使用 [SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega) 插件进行代理. (sslocal 相当于实现了 socks5 协议的server端, SwitchyOmega 相当于实现了 socks5 的 client 端)

以下为配置方式:
![proxy模式](/images/switchyOmega_proxy.jpg)
![auto-proxy模式](/images/switchyOmega_auto.jpg)
>规则列表网址: https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt

## 2. Terminal 代理

> sslocal 运行后, 终端并不会直接走 socks5 代理, 需要使用cli工具 [proxychains](https://github.com/rofl0r/proxychains-ng) 进行终端代理. (作用等同于chrome插件 SwitchyOmega)
- 安装
```bash
# Linux
sudo apt install proxychains

# Mac
brew install proxychains-ng
```
备用安装方案: 源码编译
```bash
git clone https://github.com/rofl0r/proxychains-ng.git
cd proxychains-ng
# needs a working C compiler, preferably gcc
./configure --prefix=/usr --sysconfdir=/etc
make
make install
make install-config (installs proxychains.conf)
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

## 3. SSH 配置代理
创建配置文件 `~/.ssh/config`
```
Host <指定的要走代理的域名>
  ProxyCommand=nc -X 5 -x localhost:1080 %h %p
```

## 4. Git 配置代理
> git repo主要使用两种协议：http, ssh; 
### 4.1 对于http协议的git repo

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

### 4.2 对于ssh协议的git repo
> 同 2.3 SSH 配置代理

### 4.3 配置代理的scope
对于git全局用 `git config --global`

对于当前repo用 `git config --local`

参考：
- https://segmentfault.com/q/1010000000118837
- https://www.mikeheijmans.com/sysadmin/2014/08/12/proxy-ssh-over-socks/

## 5. Gradle 配置代理
创建 `gradle` 全局配置文件 `~/.gradle/gradle.properties`
输入以下内容
```bash
org.gradle.jvmargs=-DsocksProxyHost=127.0.0.1 -DsocksProxyPort=1080
```
