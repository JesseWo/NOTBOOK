# 全局搜索框
[spotlight]()
[Alfred](https://xclient.info/s/alfred.html)
[cerebro](https://github.com/KELiON/cerebro)
开源, electric

[zazu](http://zazuapp.org/)

[listary](https://www.listary.com/)
Windows用

# finder扩展
## [Go2Shell](https://zipzapmac.com/go2shell)
> 作为finder的插件形式存在, 点击可以 打开默认的Terminal并 cd 到当前目录

## 空格键快速预览
[quick-look-plugins](https://github.com/sindresorhus/quick-look-plugins)
> 在finder里选中文件, 按space可以进行预览, 那么这些插件就是用来扩展这个预览功能的.
比如预览代码文件语法高亮, 预览APK信息, 预览格式化的markdown / json文件, 预览mac上的 .app文件内容....

# 包管理工具
[Homebrew](https://github.com/Homebrew)

# 截图
## mac自带截图功能
- 全屏截图 cmd + shift + 3
- 选中区域截图 cmd + shift + 4
- 默认存储路径 ~/Desktop
- 修改默认存储路径的方式: Terminal中输入
```
defaults write com.apple.screencapture location 自定义路径
killall SystemUIServer
```

## 长截图(滚动截图)
http://jietu.qq.com/

## 菜单栏
[stats](https://github.com/exelban/stats)
> 用于在菜单栏展示CPU/GPU/Memo/Net等系统状态信息, istat menus 的开源替代产品, 个人认为要比 istat 好用;

# 输入法
个人认为输入法是数据泄露的重灾区, 搜x百x等输入法将你的个人输入数据上传到云端, 用于广告推荐, 甚至做更大的恶也不一定; 所以需要寻找开源方案: [Rime](https://rime.im/)

Rime 只是输入法框架, 还需要搭配👇配置文件一起使用, 
> 雾凇配置文件 [rime-ice](https://github.com/iDvel/rime-ice)

在 Mac 端可以用一键部署脚本来配置 [rime-auto-deploy](https://github.com/Mark24Code/rime-auto-deploy)
```bash
git clone --depth=1 https://github.com/Mark24Code/rime-auto-deploy.git --branch latest

# install or update
cd rime-auto-deploy
./installer.rb
```


在 Android端则需要另外一款app [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android), 可以通过 F-droid 下载, 一个是 fcitx5 输入法本体apk, 另一个是 rime plugin apk, 两个都需要安装;
增加 [rime-ice] 配置: 将上述配置文件, 也就是 [rime-ice] 整个仓库zip下载下来, 然后解压到手机👇这个目录
```
/android/data/org.fcitx.fcitx5.android/files/data/rime
```
这个目录不是所有的文件管理器都能有权限访问, 推荐使用 EX文件管理器 或者 RS文件管理器, (都是当年ES文件管理器的翻版) 或者直接数据线连接PC来操作.

然后重新部署即可;

> Android 端具体安装教程见 https://1900.live/last-puzzle-android-rime-input/


多端数据同步
- Android端需要同步的是 `/android/data/org.fcitx.fcitx5.android/files/data/rime/sync` 这个文件夹, 
- Mac端需要同步的文件夹默认是 `~/Library/Rime/sync`, 当然可以修改路径, 具体在 `~/Library/Rime/installation.yaml` 的 sync_dir 字段. 

主要就是各个端上的这个文件夹保持同步, 也就是 有变动/定期同步到云端;

Android端需要搭配 foldersync 一起使用, 将 `/android/data/org.fcitx.fcitx5.android/files/data/rime/sync` 与 Google drive 里的 `rime_sync` 文件夹建立双向同步;
Mac端直接修改上述`~/Library/Rime/installation.yaml` 的 sync_dir 字段即可. 这里可以改成 Google dirve 里面的 `rime_sync` 文件夹;
如此便实现了多端同步, 但是这里同步是是个人配置项, 或者说个人数据, 比如自定义的某些快捷输入指令, 或者输入历史等, 并不是上述所有的 rime-rice 配置.

# 欧路词典
### 1. 下载
> 请使用官网下载链接; 不要用 app store (里面是免费的 lite 版和收费版本);
- [官网下载](https://www.eudic.net/v4/en/app/download)

### 2. 修改 .plist 文件实现激活
eudic 的 .plist 文件是二进制格式, 不是文本, 所以用vscode等文本编辑器无法查看和编辑; 需要下载 xcode 和 PlistEdit Pro 等来编辑; 
这里我们采用最简单的方式: CLI.
```bash
# 修改可用天数
defaults write ~/Library/Preferences/com.eusoft.eudic.plist MAIN_TimesLeft -int 820711
# 查看可用天数
defaults read ~/Library/Preferences/com.eusoft.eudic.plist MAIN_TimesLeft
```

cmd + i 查看文件简介, 修改权限为只读, 并且☑️锁定

### 3. 重启app
安装[扩展词库](https://pan.baidu.com/share/init?surl=jok5W9JOsqGlD6rQW5JRPw&pwd=rita)
- 朗文
- 牛津
- 柯林斯
