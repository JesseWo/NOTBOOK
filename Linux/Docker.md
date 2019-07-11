# Docker [官网cn](https://www.docker-cn.com/)
### 1. [安装CE社区版](https://docs.docker.com/install/linux/docker-ce/ubuntu/), 首先确认系统是否支持, 针对ubuntu系统必须是以下的64位版本
```
Artful 17.10 \(Docker CE 17.11 Edge and higher only\) Xenial 16.04 \(LTS\) Trusty 14.04 \(LTS\)
```

### 2. 安装
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

### 3. 镜像加速
国内从 Docker Hub 拉取镜像有时会遇到困难，此时可以配置镜像加速器。

* [Azure 中国镜像 https://dockerhub.azk8s.cn](https://github.com/Azure/container-service-for-azure-china/blob/master/aks/README.md#22-container-registry-proxy)
* [阿里云加速器(需登录账号获取)](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)
* [七牛云加速器 https://reg-mirror.qiniu.com](https://kirk-enterprise.github.io/hub-docs/#/user-guide/mirror)

由于镜像服务可能出现宕机，建议同时配置多个镜像。

#### 3.1 Ubuntu 16.04+、Debian 8+、CentOS 7
对于使用 `systemd` 的系统，请在 `/etc/docker/daemon.json` 中写入如下内容（如果文件不存在请新建该文件）
```bash
{
  "registry-mirrors": [
    "https://dockerhub.azk8s.cn",
    "https://reg-mirror.qiniu.com"
  ]
}
```
注意，一定要保证该文件符合 json 规范，否则 Docker 将不能启动。

之后重新启动服务。
```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

#### 3.2 Mac
打开preference, 修改如下, 然后Apply&Restart
![image.png](https://upload-images.jianshu.io/upload_images/1200965-9da0e9f2c038d0c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/340)


### 4. docker-compose
- [Github](https://github.com/docker/compose)
- [官方文档](https://docs.docker.com/compose/)
> Compose is a tool for defining and running multi-container Docker applications.

```shell
# 下载Docker Compose的最新版本 
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 添加可执行权限 
sudo chmod +x /usr/local/bin/docker-compose 
# 查看 
docker-compose --version

```

### 5. 命令行自动补全 [Command-line completion](https://docs.docker.com/compose/completion/)

    对于zsh

- 5.1 在用户home目录
```bash
mkdir -p ~/.zsh/completion 
curl -L [https://raw.githubusercontent.com/docker/compose/1.21.2/contrib/completion/zsh/\_docker-compose](https://raw.githubusercontent.com/docker/compose/1.21.2/contrib/completion/zsh/_docker-compose) &gt; ~/.zsh/completion/\_docker-compose
```

- 5.2 然后在 `~/.zshrc` 中添加
```
fpath=\(~/.zsh/completion $fpath\) autoload -Uz compinit && compinit -i
```

- 5.3 最后重启shell
```bash
exec $SHELL -l
```

### 6. [Manage Docker as a non-root user](https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user)
> Docker 需要用户具有 sudo 权限，为了避免每次命令都输入sudo，可以把用户加入 Docker 用户组


# Refs.
容器相关实现原理