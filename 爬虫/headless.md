# headless
## 1. phantomjs
  > Suspend development

Refs:
- [phantomjs Github](https://github.com/ariya/phantomjs)
- [phantomjs 官网](https://phantomjs.org/)
- [phantomjs-prebuilt NPM](https://www.npmjs.com/package/phantomjs-prebuilt)
- [phantomjs 教程(阮一峰)](https://javascript.ruanyifeng.com/tool/phantomjs.html)
- [phantomjscloud](https://phantomjscloud.com/index.html)

## 2. Headless Chrome
- [Getting Started with Headless Chrome](https://developers.google.com/web/updates/2017/04/headless-chrome)
- [Getting Started with Headless Chrome(中文)](https://zhuanlan.zhihu.com/p/29207391)

#### `Headless Chrome` 与 `PhantomJS` 的联系与区别?

> `Headless Chrome` is similar to tools like `PhantomJS`. Both can be used for automated testing in a headless environment. The main difference between the two is that Phantom uses an older version of WebKit as its rendering engine while Headless Chrome uses the latest version of Blink.<br/><br/>
At the moment, Phantom also provides a higher level API than the DevTools protocol.

#### chrome 普通模式与 headless 的区别
1. user-agent
```bash
# normal
Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.50 Safari/537.36
# headless
Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) HeadlessChrome/60.0.3112.50 Safari/537.36
```
可以自定义 UA 
```bash
chrome --headless --remote-debugging-port=9222 --user-agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.50 Safari/537.36" https://weixin.sogou.com/weixin\?query\=diqiuzhishiju
```
2. 其他标记


### ubuntu 安装 chrome
```
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - 
sudo sh -c 'echo "deb https://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
sudo apt-get update
sudo apt-get install google-chrome-stable
```
参考
- [安装: 3rd Party Repository: Google Chrome](https://www.ubuntuupdates.org/ppa/google_chrome)

# selenium
简介:
  > Selenium is an umbrella project encapsulating a variety of tools and libraries enabling web browser automation. Selenium specifically provides infrastructure(基础设施) for the W3C WebDriver specification — a platform and language-neutral coding interface compatible with all major web browsers.

[Github](https://github.com/SeleniumHQ/selenium)

## [WebDriver Specification](https://w3c.github.io/webdriver/)
具体实现:
- [ChromeDriver (selenium/wiki)](https://github.com/SeleniumHQ/selenium/wiki/ChromeDriver)
  > Developed in collaboration with the Chromium team, ChromeDriver is a standalone server which implements WebDriver's wire protocol. ChromeDriver is available for Chrome on Android and Chrome on Desktop (Mac, Linux, Windows and ChromeOS).  

- [ChromeDriver 官网](https://sites.google.com/a/chromium.org/chromedriver/)
- [The current implementation status of the WebDriver standard](https://chromium.googlesource.com/chromium/src/+/master/docs/chromedriver_status.md)
- [chromedriver 各版本下载](https://sites.google.com/a/chromium.org/chromedriver/downloads)

## [running selenium with headless chrome](https://intoli.com/blog/running-selenium-with-headless-chrome/)

# 代理工具(CLI)
## mitmproxy
- [Github](https://github.com/mitmproxy/mitmproxy)
- [docs](https://docs.mitmproxy.org/stable/)

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
