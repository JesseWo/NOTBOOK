源码
https://github.com/coolsnowwolf/lede
https://github.com/kenzok8/openwrt-packages?tab=readme-ov-file

### 如何编译
头三个选择AT91-sama5-ama5d3, 即:
```
Target System (Microchip (Atmel AT91))  --->
(X) Microchip (Atmel AT91)
Subtarget (SAMA5D3 boards(Cortex-A5))  --->
(X) SAMA5D3 boards(Cortex-A5)
Target Profile (Microchip(Atmel AT91) SAMA5D3 Xplained)  --->
(X) Microchip(Atmel AT91) SAMA5D3 Xplained  
```

6，下载 dl 库，编译固件 （-j 后面是线程数）
```bash
# 下载dl库，V=s 显示任务详细情况
make -j8 download V=s       
# 4代表线程，根据个人实际情况调整              
make V=s -j4           
```                           


### 如何将自编译的openwrt固件直接导入玩客云docker内运行
编译完成后大家会得到两个压缩的文件sdcard是U盘SD卡使用的，另外个rootfs.tar结尾的就是docker使用的。
安装步骤：
安装 Armbian 后
更新软件（非必要）
```bash
apt-get update && apt-get upgrade
```
安装 Docker
```bash
apt install docker.io
```
打开网卡混杂模式
```bash
ip link set eth0 promisc on
```
创建网络
```bash
docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 macnet
```
[↑自己根据 玩客云 所在网段修改，如：玩客云IP:192.168.2.175，则192.168.1.0/24 改成 192.168.2.0/24，192.168.1.1改成主路由地址]

由于我们是使用本地编译的固件直接安装后面的就可以不参照他的了。
将本地编译的openwrt-at91-sama5-microchip_sama5d3-xplained-rootfs.tar上传到玩客云根目录下（其他目录参照修改）
创建容器镜像
```bash
docker import /openwrt-at91-sama5-microchip_sama5d3-xplained-rootfs.tar.gz lean_openwrt
```
结尾的lean_openwrt为镜像名，可以随意改变为自己喜欢的。
启动容器
```bash
docker run -itd --name=openwrt --restart=always --network=macnet --privileged=true lean_openwrt /sbin/init
```
更改openwrt管理地址配置
```bash
docker exec -it openwrt /bin/sh
```
编辑 /etc/config/network
找到lan下的option ipaddr改为自己对应的管理IP
重启OpenWRT网络服务
```bash
/etc/init.d/network restart
```
推出docker
```bash
exit
```
重启网卡生效
```bash
/etc/init.d/networking restart
```
