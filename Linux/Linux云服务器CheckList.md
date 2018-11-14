# Linux云服务器CheckList

目前云服务器系统主要分为两种: Ubuntu 和 CentOS, 两者都是基于Linux内核的发行版. 对于小白用户, 以下是最基本的区别...

| 系统 | 系列 | 包管理器 | 备注 |
| :---: | :---: | :---: | :---: |
| Ubuntu | Debian | yum | 在桌面应用方面做得好 |
| CentOS | Redhat | apt | 企业级用户较多,稳定性好 |

当然根据自己的个人习惯, 我还是选择了Ubuntu

### 0. vps选择调研

知乎: [国外或香港有哪些好用的 VPS 或者独立主机？](https://www.zhihu.com/question/21432244) 赵荣部落: [精选便宜VPS主机](http://www.zrblog.net/10dao)

我最终选择了这个 [vermach](https://virmach.com/), $12/年 以下为本人选用的vps信息

```text
uname -a
Linux jessewo 4.10.12-041012-generic #201704210512 SMP Fri Apr 21 09:14:40 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux

cat /etc/issue
Ubuntu 14.04.5 LTS
```

### 1. 基本配置

#### 1.1 ssh配置免登陆

```bash
#在你本机, 将ssh公钥上传到vps, 以下命令回车后输入登录密码
ssh-copy-id root@your_vps_ip
```

具体参见 [Linux免密码SSH登录（公钥登录）](https://www.jianshu.com/p/7f5f727a2b60)

#### 1.2 配置安全组规则\(针对阿里云服务器\)

当你发现自己搭建的http服务, 通过本地回环地址\(127.0.0.1\)可以访问, 通过公网IP却没法访问时, 第一时间肯定想到了是防火墙作祟, 但当用 `iptables -t filter -L` 查看 `filter` 表的规则却是空的...好诡异! 后来发现在阿里云控制台可以配置防火墙规则....md 默认情况下, 入方向只允许SSH\(22端口\)访问, 若需开启http/https/ftp/mysql以及其他自定义服务, 需要针对入方向进行单独配置. [阿里云官方文档](https://help.aliyun.com/document_detail/25475.html?spm=5176.2020520101.0.0.50e54df5t5hHzl#concept_ngr_vht_xdb__allowHttp)

#### 1.3 解决ssh超时自动断连的问题

若你的服务器没遇到此问题, 那么可以忽略.

```bash
#修改ssh的配置文件
vim /etc/ssh/sshd_config

#添加如下两行配置
#服务端每隔60s给client发送心跳包
ClientAliveInterval 60  
#服务器发出请求后客户端没有响应的次数达到3次, 就自动断开
ClientAliveCountMax 3
```

### 2. 基础模块的安装

* curl
* wget 
* vim 
* git 
* screen
* db-util
* openssl

  ```bash
  apt install -y curl wget vim git screen db-util openssl
  ```

* zsh 

  ```bash
  #安装 zsh
  apt install zsh
  #切换为zsh
  chsh -s `which zsh`
  #安装 oh-my-zsh (美化)
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-    zsh/master/tools/install.sh)"
  #重连ssh后 查看当前shell
  echo $SHELL
  ```

* 内网穿透 [frp](https://github.com/fatedier/frp/blob/master/README_zh.md)
* 安装语言包解决如下问题:

  ```text
  perl: warning: Setting locale failed.
  perl: warning: Please check that your locale settings:
    LANGUAGE = (unset),
    LC_ALL = (unset),
    LC_CTYPE = "zh_CN.UTF-8",
    LANG = "en_US.UTF-8"
    are supported and installed on your system.
  perl: warning: Falling back to a fallback locale ("en_US.UTF-8").
  ```

  ```bash
  apt install language-pack-zh-hans
  ```

* FTP

  [ubuntu搭建ftp服务](https://www.jianshu.com/p/dec051c3f878)

* [SSMTP](https://wiki.archlinux.org/index.php/SSMTP)

### 3. 开发环境配置

* **python**

  ```bash
  apt install python python3
  ```

* **node**

  ```bash
  #node版本管理器 nvm
  curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
  #安装最新node LTS版本
  nvm install --lts
  #更新npm版本
  npm i -g npm
  ```

  淘宝[cnpm](https://npm.taobao.org/)

  ```bash
  npm install -g cnpm --registry=https://registry.npm.taobao.org
  ```

* **openjdk**

  jre

  ```text
   apt install openjdk-8-jre
  ```

  jdk

  ```text
   apt install openjdk-8-jdk
  ```

* **gcc**

  ```text
  apt install build-essential libtool
  ```

* **Nginx**
* **Mysql**
  ```bash
  #安装server端
  apt install mysql-server
  #配置MySQL
  mysql_secure_installation
  #启动
  service mysql start
  #安装client端
  apt install mysql-client
  ```

- #### [mangoDB](https://www.mongodb.com) 
    * [中文一](http://www.mongodb.org.cn/tutorial/56.html)
    * [中文二](http://www.mongoing.com/docs/tutorial/install-mongodb-on-ubuntu.html)


- [Redis](https://redis.io/)    ([中文](http://www.redis.cn))
1. 安装
```bash
wget http://download.redis.io/releases/redis-5.0.0.tar.gz
tar xzf redis-5.0.0.tar.gz
cd redis-5.0.0
make
```
2. 使用
>使用 `Systemd` 来管理, service单元脚本在 /etc/systemd/system/下
```bash
service redis-server start
service redis-server status
service redis-server stop
service redis-server restart
# 设置开机自启
systemctl enable redis-server
```

- #### Docker [官网cn](https://www.docker-cn.com/)
1. [安装CE社区版](https://docs.docker.com/install/linux/docker-ce/ubuntu/), 首先确认系统是否支持, 针对ubuntu系统必须是以下的64位版本
```
Artful 17.10 \(Docker CE 17.11 Edge and higher only\) Xenial 16.04 \(LTS\) Trusty 14.04 \(LTS\)
```

2. 安装
```bash
#Update the apt package index:
sudo apt-get update
#Install packages to allow apt to use a repository over HTTPS:
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
#Add Docker’s official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
#set up the stable repository. (x86_64/amd64)
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
#Update the apt package index.
sudo apt-get update
#install the latest version of Docker CE
sudo apt-get install docker-ce
#查看版本
docker -v
#Docker version 18.03.1-ce, build 9ee9f40
```

3. 配置镜像
打开/etc/default/docker文件（需要sudo权限)，在文件的底部加上一行。
```
DOCKER\_OPTS="--registry-mirror=[https://registry.docker-cn.com](https://registry.docker-cn.com)"
```

然后重启
```
service docker restart
```
对于mac, 打开preference, 修改如下, 然后Apply&Restart
![image.png](https://upload-images.jianshu.io/upload_images/1200965-9da0e9f2c038d0c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/340)

参考: [Docker 中国官方镜像加速](https://www.docker-cn.com/registry-mirror)

4. 安装 [docker-compose](https://docs.docker.com/compose/install/#install-compose)
```
//下载Docker Compose的最新版本 sudo curl -L [https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$\(uname](https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$%28uname) -s\)-$\(uname -m\) -o /usr/local/bin/docker-compose //添加可执行权限 sudo chmod +x /usr/local/bin/docker-compose //查看 docker-compose --version

```

5. 命令行自动补全 [Command-line completion](https://docs.docker.com/compose/completion/)

#### 5. zsh
5.1. 在用户home目录
```bash
mkdir -p ~/.zsh/completion curl -L [https://raw.githubusercontent.com/docker/compose/1.21.2/contrib/completion/zsh/\_docker-compose](https://raw.githubusercontent.com/docker/compose/1.21.2/contrib/completion/zsh/_docker-compose) &gt; ~/.zsh/completion/\_docker-compose
```

5.2. 然后在 ```~/.zshrc``` 中添加
```
fpath=\(~/.zsh/completion $fpath\) autoload -Uz compinit && compinit -i
```

5.3. 最后重启shell
```bash
exec $SHELL -l
```

## 4. 梯子
---
### 4.1 SS (境外服务器上安装)
  * **Install**   [Github地址](https://github.com/shadowsocks)
  * **Config**
  ```vim /etc/shadowsocks.json
```

* **Optimize**

  [Optimizing-Shadowsocks](https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks)

  [TCP-Fast-Open](https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open)

* **Log**

  `less /var/log/shadowsocks.log`

[raspberrypi](https://www.jianshu.com/p/87f19de08877)

#### 4.2 加速

**4.2.1 锐捷加速**

[https://www.freehao123.com/vps-net-speeder-serverspeeder/](https://www.freehao123.com/vps-net-speeder-serverspeeder/) [https://www.91yun.org/serverspeeder91yun](https://www.91yun.org/serverspeeder91yun)

**4.2.2 谷歌BBR加速\(✨\)**

Google开源TCP BBR拥塞控制算法（简称BBR），可以应用到常规的KVM和XEN架构的VPS、服务器中，用来提升服务器的速度。 [Ubuntu升级内核,开启BBR加速](https://leiquan.website/2017/04/24/Ubuntu开启BBR加速Shadowsocks/) **需升级内核，五星推荐，实测效果非常明显（ping值虽没有明显改善，但下行速度提升相当明显）。** 打开视频，自动切换为1080P，无压力 ![Paste\_Image.png](http://upload-images.jianshu.io/upload_images/1200965-814855105f202ab5.png?imageMogr2/auto-orient/strip|imageView2/2/w/720)

因新升级后的内核版本过高，锐捷加速不支持此内核。所以目前两种加速方式只能二选一 1.2

**4.2.3 SS中继加速\(境内服务器上安装\)**

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
[以上参考](https://doub.io/ss-jc29/)

