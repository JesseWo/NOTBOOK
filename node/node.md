
## node
- [npm官方文档](https://docs.npmjs.com/)
- [npm: package.json](https://docs.npmjs.com/files/package.json)
- [npm scripts 使用指南](http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html)
- [koa](https://koa.bootcss.com/)

## 内存缓存
- [Redis](http://www.redis.net.cn/)
- [node-Redis](https://www.npmjs.com/package/redis)

## 数据库
- [MongoDB](https://docs.mongodb.com/guides/)
- [MongoDB 中文](http://www.mongodb.org.cn/tutorial/)
- [mongoose](http://mongoosejs.com/docs/index.html)

## 开源分布式存储
### 1. 调研资料
```
分布式存储按其存储接口分为三种：文件存储、块存储和对象存储。

文件存储
通常支持POSIX接口（如glusterfs，但GFS、HDFS是非POSIX接口的），可以像普通文件系统（如ext4）那样访问，但又比普通文件系统多了并行化访问的能力和冗余机制。主要的分布式文件存储系统有TFS、cephfs、glusterfs和HDFS等。主要存储非结构化数据，如普通文件、图片、音视频等。可以采用NFS和CIFS等协议访问，共享方便。NAS是文件存储类型。

块存储
这种接口通常以QEMU Driver或者Kernel Module的方式存在，主要通过qemu或iscsi协议访问。主要的块存储系统有ceph块存储、sheepdog等。主要用来存储结构化数据，如数据库数据。数据共享不方便。DAS和SAN都是块存储类型。

对象存储
对象存储系统综合了NAS和SAN的优点，同时具有SAN的高速直接访问和NAS的数据共享等优势。以对象作为基本的存储单元，向外提供RESTful数据读写接口，常以网络服务的形式提供数据访问。主要的对象存储系统有AWS、swift和ceph对象存储。主要用来存储非结构化数据。
```
### 参考
- [阿里云OSS相关基本概念介绍](https://help.aliyun.com/document_detail/31827.html?spm=a2c4g.11186623.2.17.3d2c491dhNZcL5#concept-izx-fmt-tdb)
- [开源分布式存储系统的对比](https://blog.csdn.net/zzq900503/article/details/80020725)
- [为什么对象存储在蚕食世界？](https://www.zhihu.com/question/48259783)
- [glusterfs：优秀开源分布式存储系统](https://zhuanlan.zhihu.com/p/45060910)

### 2. 开源项目
- ceph
    - [docs](http://docs.ceph.com/docs/master/start/intro/)
    - [github](https://github.com/ceph/ceph)
- GlusterFS
- OpenStack Swift
- minio
    > 简约的对象存储服务器系统，与亚马逊S3实现了API兼容。Minio用Go编写而成，这是一种轻量级、高度并发的解决方案.
    - [docs](https://minio.io/)
    - [github](https://github.com/minio)

- 其他
    - oss-server (java实现)
        > 简易开源项目, 目测是基于文件系统, 非oss
        - [docs](http://oss-server.mydoc.io/)
        - [github](https://github.com/xiaoymin/oss-server)

## 用户系统设计
### 1. 登录验证码生成
- 短信/邮箱验证码
    - [短UUID生成: hashids](https://github.com/ivanakimov/hashids.js)
    - [nodemail: 发邮件](https://nodemailer.com/about/)
- [图形验证码: svg-captcha](https://github.com/lemonce/svg-captcha/blob/HEAD/README_CN.md)
- 验证码攻击防范
    [5种常见的短信验证码防刷策略](http://www.woshipm.com/pd/580976.html)
    

### 2. token生成
- [sessionID生成: node-uuid UUID生成(RFC4122)](https://github.com/kelektiv/node-uuid)
    - 防重复原理
- [json web token](https://github.com/auth0/node-jsonwebtoken)
- [koa-session2](https://github.com/Secbone/koa-session2#readme)
- API token (内部服务api调用)
    //todo

### 3. 密码安全
- 存储安全
    - [加盐密码哈希：如何正确使用](http://blog.jobbole.com/61872/)
    - [密码存储加密: 慢哈希算法介绍以及各语言的实现](https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016#nodejs)
    - [node: bcrypt](https://www.npmjs.com/package/bcrypt)
- 传输安全
    - https
    - 加密传输

## 其他
- [二维码生成: qrcode.react](https://github.com/zpao/qrcode.react)
- [apk和ipa包解析: isomorphic-pkg-reader](https://www.npmjs.com/package/isomorphic-pkg-reader)

## 优秀项目
- [Nodeclub: 使用 Node.js 和 MongoDB 开发的社区系统](https://github.com/cnodejs/nodeclub)
- [react 后台管理系统解决方案](https://github.com/yezihaohao/react-admin)