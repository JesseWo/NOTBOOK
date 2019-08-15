
## node
- [npm官方文档](https://docs.npmjs.com/)
- [npm: package.json](https://docs.npmjs.com/files/package.json)
- [npm scripts 使用指南](http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html)
- [koa](https://koa.bootcss.com/)
- [TypeScript体系调研报告](https://juejin.im/post/59c46bc86fb9a00a4636f939)

## 脚手架
- [eggjs](https://github.com/eggjs/egg)
- [TypeScript-Node-Starter](https://github.com/microsoft/TypeScript-Node-Starter)
- [node-typescript-boilerplate](https://github.com/jsynowiec/node-typescript-boilerplate)


## 命令行
- [shelljs](https://github.com/shelljs/shelljs)
- [commander.js](https://github.com/tj/commander.js)

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
- 二维码生成
    - [qrcode.react](https://github.com/zpao/qrcode.react)
    - [生成中间带LOGO的二维码: qrcode-logo](https://github.com/fisherw/qrcode-logo)
    - 图片合成
        - [GraphicsMagick](http://www.graphicsmagick.org/)
        - [node: gm](https://github.com/aheckmann/gm)
        - [node服务器如何生成有logo和背景的带参数二维码](https://blog.csdn.net/AF52520/article/details/77971653)

- [apk 和 ipa 包解析: isomorphic-pkg-reader](https://www.npmjs.com/package/isomorphic-pkg-reader)
    - [isomorphic-pkg-reader 改进增强版](https://github.com/JesseWo/isomorphic-pkg-reader)
    - [isomorphic-unzip](http://npm.taobao.org/package/isomorphic-unzip)
    - 提取ipa中的icon
        > ipa中的icon虽然为png格式, 但此png格式不同于普通的png, Apple对png图片进行了了自定义的[pngcrush](https://pmt.sourceforge.io/pngcrush/) 压缩, 故此格式的图片在非apple的软件内无法正常显示.
        
        - PNG格式
            - [REC-PNG-20031110: PNG格式标准](https://www.w3.org/TR/2003/REC-PNG-20031110/)
            - [PNG-Structure](http://www.libpng.org/pub/png/spec/1.0/PNG-Structure.html)
            - [png.js](https://github.com/TencentWSRD/png.js)
        - CgBI格式
            - [CgBI_file_format](http://iphonedevwiki.net/index.php/CgBI_file_format)
            - Implementations
                - Encoding
                    - [pincrush (c实现)](https://github.com/DHowett/pincrush)
                - Decoding
                    - [pngdefry (c实现)](http://www.jongware.com/pngdefry.html)
                    - [node-pngdefry (对 pngdefry 的node封装)](https://github.com/forsigner/node-pngdefry)
                    - [iPhone PNG Image Normalizer (python实现)](https://axelbrz.com/?mod=iphone-png-images-normalizer)
                    
        

## 参考项目
- [Nodeclub: 使用 Node.js 和 MongoDB 开发的社区系统](https://github.com/cnodejs/nodeclub)
- [react 后台管理系统解决方案](https://github.com/yezihaohao/react-admin)
- [教你搭建App内测下载平台](https://www.jianshu.com/p/48b38a2d0bbb)