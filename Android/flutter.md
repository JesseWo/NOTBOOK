
#### install
```bash
brew install flutter --cask
```

#### 查看安装位置
```bash
which flutter

➜  ~ which flutter
/opt/homebrew/bin/flutter
```

#### 查看当前flutter环境
```bash
flutter doctor -v

➜  ~ flutter doctor -v
[✓] Flutter (Channel stable, 3.0.3, on macOS 12.4 21F79 darwin-arm, locale zh-Hans-CN)
    • Flutter version 3.0.3 at /opt/homebrew/Caskroom/flutter/3.0.2/flutter
    • Upstream repository https://github.com/flutter/flutter.git
    • Framework revision 676cefaaff (9 days ago), 2022-06-22 11:34:49 -0700
    • Engine revision ffe7b86a1e
    • Dart version 2.17.5
    • DevTools version 2.12.2

[✓] Android toolchain - develop for Android devices (Android SDK version 32.1.0-rc1)
    • Android SDK at /Users/user/Library/Android/sdk
    • Platform android-32, build-tools 32.1.0-rc1
    • ANDROID_HOME = /Users/user/Library/Android/sdk
    • Java binary at: /Applications/Android Studio.app/Contents/jre/Contents/Home/bin/java
    • Java version OpenJDK Runtime Environment (build 11.0.12+0-b1504.28-7817840)
    • All Android licenses accepted.

[✓] Xcode - develop for iOS and macOS (Xcode 13.4.1)
    • Xcode at /Applications/Xcode.app/Contents/Developer
    • CocoaPods version 1.11.3

[✓] Chrome - develop for the web
    • Chrome at /Applications/Google Chrome.app/Contents/MacOS/Google Chrome

[✓] Android Studio (version 2021.2)
    • Android Studio at /Applications/Android Studio.app/Contents
    • Flutter plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/9212-flutter
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart
    • Java version OpenJDK Runtime Environment (build 11.0.12+0-b1504.28-7817840)

[✓] VS Code (version 1.68.1)
    • VS Code at /Applications/Visual Studio Code.app/Contents
    • Flutter extension version 3.42.0

[✓] Connected device (3 available)
    • MI 9 (mobile)   • f6bb80b6 • android-arm64  • Android 11 (API 30)
    • macOS (desktop) • macos    • darwin-arm64   • macOS 12.4 21F79 darwin-arm
    • Chrome (web)    • chrome   • web-javascript • Google Chrome 103.0.5060.53

[✓] HTTP Host Availability
    • All required HTTP hosts are available

• No issues found!
```

#### 查看所有分支
```bash
flutter channel

➜  ~ flutter channel
Flutter channels:
  master
  beta
* stable
```

#### 更新Flutter SDK和flutter项目依赖包
```bash
flutter upgrade
```

#### 创建并运行模板app
```bash
flutter create my_app
cd my_app 
flutter run
```

### Refs.
- [flutter macos install](https://docs.flutter.dev/get-started/install/macos)
