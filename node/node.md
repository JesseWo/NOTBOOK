
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

### 3. 密码安全
- 存储安全
    - [加盐密码哈希：如何正确使用](http://blog.jobbole.com/61872/)
    - [密码存储加密: 慢哈希算法介绍以及各语言的实现](https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016#nodejs)
    - [node: bcrypt](https://www.npmjs.com/package/bcrypt)
- 传输安全
    - https
    - 加密传输


## 优秀项目
- [Nodeclub: 使用 Node.js 和 MongoDB 开发的社区系统](https://github.com/cnodejs/nodeclub)
- [react 后台管理系统解决方案](https://github.com/yezihaohao/react-admin)