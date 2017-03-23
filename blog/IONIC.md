# Ionic 环境搭建

## 1.ionic 介绍

## 2.android 环境搭建
### 安装node.js
nodejs官网 `https://nodejs.org/` 下载最新版本的node.js。
安装完后输入` node -v ` 查看是否安装成功 。
#### 安装cnpm
因为npm的源在国外，所以速度很慢，没有代理的同学可以使用淘宝镜像速度快很多。
>  npm install -g cnpm --registry=https://registry.npm.taobao.org

安装成功后把命令里的 `npm` 换成 `cnpm` 即可。

### 安装ionic
使用node.js 的包管理器npm安装ionic。
> npm install -g ioinc

安装完之后输入 `ionic -v` 查看ionic 版本。

输入 `ionic info` 查看ionic信息。

#### 安装cordova
> npm install -g cordova

输入 `cordova -v` 查看是否安装成功。

#### 第一个APP
ionic自带了很多demo，先下载一个看看。
> ionic start cutePuppyPics --v2

##### 启动
下载成功后，切换到项目目录，然后启动服务，服务成功启动后ionic会自动在浏览器打开页面。
```
cd cutePuppyPics/
ionic serve
```

### 安装 JAVA和ANDROID SDK
现在还只能在浏览器中预览，要把demo编译成手机能安装的APP还需要JAVA和ANDROID SDK。
#### 安装JAVA
1. 根据操作系统版本在  [java官网](http://www.oracle.com/technetwork/java/javase/downloads/index.html "JAVA官网") 下载sdk。
2. 在系统->环境变量 中新建 `JAVA_HOME` ，然后把 `%JAVA_HOME%` 添加到 `path` 中。
3. 在命令行输入 ` java -v` 查看是否安装成功。

#### 安装 android studio
1. 下载包含Android Sdk的版本，[Android Studio](http://www.android-studio.org/ "Android Studio")。
2. 在系统->环境变量 中新建 `ANDROID_HOME` ，然后把 `%ANDROID_HOME%`，`%ANDROID_HOME%\platform-tools`  添加到 `path` 中。
3. 在命令行中输入 `adb` 查看 `Android Sdk` 是否安装成功。
4. 打开 Android Studio 在 Tools -> Android -> Android Virtual Device Manager 新建一个模拟器。

#### 编译、启动模拟器
先在ionic中添加android平台
>ionic add platform android


在命令行中输入
>  ionic build android  

编译完之后apk生成在项目目录下 `\platforms\android\build\outputs\apk\` 下。

在模拟器中运行
> ionic emulate android  

编译加运行
>ionic run android  




## 3.ios 开发环境搭建
虽然ionic是跨平台的框架，但是ios APP只能在Mac  OS 上开发，所以你没有mac电脑的话只能先装个模拟器啦。

模拟器安装可以参考这个链接 [模拟器安装 Mac OS](http://bbs.feng.com/forum.php?mod=viewthread&tid=10620016)。

### node.js 、ionic 安装
步骤与android的类似，记得命令前加上 `sudo` 即可。

### 安装xcode
在app store 中搜索 `xcode` ，点击安装。

### 第一个IOS APP
下载 demo
> ionic start cutePuppyPics --v2

安装ios模拟器
> sudo cnpm install -g ios-sim

在ionic中添加ios 开发平台
> ionic platform add ios

编译 APP
> ionic build ios

在模拟器中调试
> ionic emulate ios 
