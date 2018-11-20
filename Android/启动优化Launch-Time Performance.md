# 启动优化(Launch-Time Performance)
App启动过程:

    
启动时间统计:
- [系统logcat(API19以上):verbose Displayed](https://developer.android.com/topic/performance/vitals/launch-time#dx)
    ```
    I/ActivityManager: Displayed com.tencent.mm/.ui.LauncherUI: +761ms
    I/ActivityManager: Displayed com.sina.weibo/.SplashActivity: +886ms
    I/ActivityManager: Displayed com.sina.weibo/.MainTabActivity: +1s562ms
    ```
- adb
    ```
    adb [-d | -e | -s <serialNumber>] shell am start -S -W 
    com.example.app/.MainActivity 
    -c android.intent.category.LAUNCHER 
    -a android.intent.action.MAIN
    ```
    例子
    ```
    # 执行
    adb shell am start -S -W com.sina.weibo/.SplashActivity -c android.intent.category.LAUNCHER -a android.intent.action.MAIN
    # 输出
    Stopping: com.sina.weibo
    Starting: Intent { act=android.intent.action.MAIN cat=[android.intent.category.LAUNCHER] cmp=com.sina.weibo/.SplashActivity }
    Status: ok
    Activity: com.sina.weibo/.SplashActivity
    ThisTime: 786
    TotalTime: 786
    WaitTime: 864
    Complete
    ```
    ThisTime, TotalTime, WaitTime 三者的区别? 
    - [怎么计算apk的启动时间？](https://www.zhihu.com/question/35487841)
    
* 自行埋点统计
    如何埋点? start和end在哪?

调试工具:
- [Google: CPU profiler](https://developer.android.com/studio/profile/cpu-profiler)
- [JakeWharton: hugo](https://github.com/JakeWharton/hugo)
- [Facebook: Stetho](http://facebook.github.io/stetho/)

实践:
1. 生命周期内减少耗时操作;
    * Application:attachBaseContext()：
    * Application:onCreate()
    * MainActiviity:onCreate()
2. 避免冷启动;
    * moveTaskToBack
3. 视觉欺骗: Splash WindowBackGround;<br/>
    关于```layer-list```和```item```,```bitmap```等xml标签的使用
    - [Android drawable](https://developer.android.com/guide/topics/resources/drawable-resource#Shape)
    - [layer-list的使用例子](https://blog.csdn.net/north1989/article/details/53485729)
    - [Android XML shape 标签使用详解](https://www.cnblogs.com/popfisher/p/6238119.html)

参考:
- [腾讯Bugly: 5分钟教你打造一个秒开的 Android App](https://mp.weixin.qq.com/s?__biz=MzA3NTYzODYzMg==&mid=2653579242&idx=2&sn=303f2469462e42b92e9fb8341d7bfd47&chksm=84b3b5edb3c43cfb8394cc381d4afb56c949106321158dac3e4e0016f5f9a6be190c612b28f2&mpshare=1&scene=1&srcid=0810OrOIZ2ZxAN8IhnhP0Wup%23rd)
- [其实你不知道MultiDex到底有多坑](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/1218/3789.html)
- [Redex初探与Interdex：Andorid冷启动优化](https://zhuanlan.zhihu.com/p/24002157)
- []()
