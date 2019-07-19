# RSS
RSS 烧录

Refs:
- [huginn Github](https://github.com/huginn/huginn)
- [huginn Docker](https://hub.docker.com/r/huginn/huginn/)
- [huginn 环境变量](https://github.com/huginn/huginn/blob/master/.env.example)
- [huginn 中文论坛](https://huginn.cn/)
- [Huginn: 烧录RSS的神器](https://cloud.tencent.com/developer/article/1405484)
- [w3schools: RSS](https://www.w3schools.com/xml/xml_rss.asp)

- [利用Huginn抓取任意网站RSS和微信公众号更新](https://wzfou.com/huginn-rss/)
- [微信公众号 scenarios](http://huginnio.herokuapp.com/scenarios/17/download)

# headless
## phantomjs
> Suspend development
Refs:
- [phantomjs Github](https://github.com/ariya/phantomjs)
- [phantomjs 官网](https://phantomjs.org/)
- [phantomjs-prebuilt NPM](https://www.npmjs.com/package/phantomjs-prebuilt)
- [phantomjs 教程(阮一峰)](https://javascript.ruanyifeng.com/tool/phantomjs.html)
- [phantomjscloud](https://phantomjscloud.com/index.html)

## Headless Chrome
- [Getting Started with Headless Chrome](https://developers.google.com/web/updates/2017/04/headless-chrome)
- [Getting Started with Headless Chrome(中文)](https://zhuanlan.zhihu.com/p/29207391)

## 关于浏览器内核
浏览器内核分为两个部分，渲染引擎(layout engineer 或者 Rendering Engine)和 JS 引擎。现在JS引擎比较独立，内核更加倾向于说渲染引擎。

- 1、Trident内核：代表作品是IE，因IE捆绑在Windows中，所以占有极高的份额，又称为IE内核或MSHTML，此内核只能用于Windows平台，且不是开源的。代表作品还有腾讯、Maxthon（遨游）、360浏览器等。但由于市场份额比较大，曾经出现脱离了W3C标准的时候，同时IE版本比较多，存在很多的兼容性问题。

- 2、Gecko内核：代表作品是Firefox，即火狐浏览器。因火狐是最多的用户，故常被称为firefox内核它是开源的，最大优势是跨平台，在Microsoft Windows、Linux、MacOs X等主   要操作系统中使用。
Mozilla是网景公司在第一次浏览器大战败给微软之后创建的。有兴趣的同学可以了解一下浏览器大战
- 3、Webkit内核：代表作品是Safari、曾经的Chrome，是开源的项目。
- 4、Presto内核：代表作品是Opera，Presto是由Opera Software开发的浏览器排版引擎，它是世界公认最快的渲染速度的引擎。在13年之后，Opera宣布加入谷歌阵营，弃用了    Presto
- 5、Blink内核：由Google和Opera Software开发的浏览器排版引擎，2013年4月发布。现在Chrome内核是Blink。谷歌还开发了自己的JS引擎，V8，使JS运行速度极大地提高了

Refs
- [Blink](https://blog.chromium.org/2013/04/blink-rendering-engine-for-chromium.html)
    > An open source rendering engine for the Chromium project, based on WebKit.
- [五大主流浏览器内核的源起以及国内各大浏览器内核总结](https://blog.csdn.net/summer_15/article/details/71249203)

# kindle
- [kindleEar](https://github.com/cdhigh/KindleEar)

kindleEar 推送服务一键部署脚本
```bash
curl -o- https://raw.githubusercontent.com/kindlefere/KindleEar-Uploader/master/uploader.sh | bash
```
  - [faq](http://kindleear.appspot.com/static/faq.html#ownserver)
  - [KindleEar 搭建教程：推送 RSS 订阅到 Kindle](https://www.imahui.com/notes/233.html)
