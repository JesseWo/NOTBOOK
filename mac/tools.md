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
个人认为输入法是数据泄露的重灾区, 搜x百x等输入法将你的个人输入数据上传到云端, 用于广告推荐, 甚至做更大的恶也不一定; 所以需要寻找开源方案:
- 开源输入法 [Rime](https://rime.im/)
- 配置文件 [rime-ice](https://github.com/iDvel/rime-ice)
- 一键部署脚本 [rime-auto-deploy](https://github.com/Mark24Code/rime-auto-deploy)
- Android端 [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android)

以上都可以给予同一份配置文件: [rime-ice]

