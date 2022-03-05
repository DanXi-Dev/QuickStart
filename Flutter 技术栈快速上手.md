# Flutter 技术栈快速上手

[TOC]

## 概念介绍

Flutter 是 Google 开发的、由社区进行维护的开源跨平台应用框架。**它不是一个编程语言，只是一套框架。它使用的语言叫`Dart`。**

Dart 是 Google 开发的、专为开发结构化应用而生的语言，它包括虚拟机、一系列的库和工具。**它是一个编程语言。**

Dart 在很多地方的语法都和`JavaScript`、`Java`、`Kotlin`、`C++`等语言有异曲同工之妙。**如果你熟悉任何一门，上手起来会简单不少。**

下面是一些总的**特征概括**。如果你没有上面这些语言基础，不看也罢；有的话，看了之后能有个大致的印象。

**一些关于 Dart 的基本特点描述（详见[这篇文章](https://www.jianshu.com/p/8a62b1a2fd75)）：**

1. 它基本上是强类型的，而不像弱类型的 Python；
2. 它的入口是`main()`，这一点和 C 语言一样；
3. 所有对象都是类。例如数字是`int`或者`double`，字符串是`String`；
4. 像 C 一样，它的变量可以写在文件的最顶层（不在任何花括号中）。这时候，这个变量相当于全局变量，可以从其他文件访问、赋值；
5. 它基本上是单线程的，你不用考虑线程的问题。如果真的要用，你可以自行百度`Flutter Isolate`获得更多说明；
6. 它自带对异步的支持。你可以使用`async/await`定义/等待异步的方法（例如网络请求等耗时操作）；
7. 它没有访问限定修饰符。如果你熟悉`Java`或者`C++`的`public`、`private`等关键字，在这里你可以忘了它们——任何变量、方法，以`_`开头就是私有的，不以`_`开头就是公共的。（想用`protected`？直接使用`@protected`注解即可）
8. 它可以编译成多种类型，例如 JavaScript 脚本和原生库。

**一些关于 Flutter 的基本特点描述：**

1. 它没有什么布局文件，所有界面布局就是用代码定义的；
2. 它使用`yaml`文件来描述项目的配置，主要是`pubspec.yaml`；
3. 它的布局是一棵树，所有有关布局的东西都在树上。树上的每一个节点既可以代表一个界面控件（例如按钮`TextButton`），可以是一个布局控件（例如可滚动视图`SingleChildScrollView`、横向布局`Row`），也可以是某种抽象的界面控件（例如点击监听器`GestureDetector`），甚至有些节点纯粹起辅助作用（例如指示子控件使用什么颜色主题的`Theme`）。

## 安装

无需多说，到 https://flutter.cn/docs/get-started/install 就可以安装 SDK。直接用最新版本即可。

大致分成几步：

1. 下载 SDK，解压到某个目录（比如`D:\SDK\Flutter\`)
2. 编辑环境变量，在`PATH`中加入`D:\SDK\Flutter\bin`这个目录（也可能是`D:\SDK\Flutter\flutter-windows-dev-1.2.3\bin`这样的，务必先查看一下）。这样你应该可以直接在命令行里运行`flutter`和`dart`。**如果编辑完后还说「未找到命令」，重启一下电脑。**
3. 编辑环境变量，添加`PUB_HOSTED_URL`和`FLUTTER_STORAGE_BASE_URL`两个环境变量，值分别是`https://pub.flutter-io.cn`和`https://storage.flutter-io.cn`。这是为了让你走国内镜像，否则 Flutter 需要翻墙而且速度很慢。
4. 到 https://developer.android.google.cn/studio 安装 Android Studio。安装完后自行配置，有问题可以先 Google 一下。
	> **建议：**
	> 直接从官网下载安装可能不是个最好的主意，有可能需要科学上网。  
	> 我个人推荐你试试 [Jetbrains Toolbox](https://www.jetbrains.com/zh-cn/toolbox-app/) 来一键安装 Android Studio，可以省去很多安装配置的冗余过程。
	
	> **我可以使用其他 IDE 吗？**  
	> 当然！[Visual Studio Code](https://code.visualstudio.com/)就很可以。如果这样，你可以忽略第 4 步和第 5 步，转而了解[如何在 VSCode 上使用 Flutter](https://flutter.cn/docs/get-started/editor?tab=vscode)。
5. 安装 Flutter 插件到 Android Studio。具体看 https://flutter.cn/docs/get-started/editor。
6. 命令行执行`flutter doctor`，根据说明看看自己还缺啥。
7. （可选）如果不希望连接手机，而是直接在 Windows 上搞测试，还要安装 Visual Studio 2022 Community。具体看https://flutter.cn/docs/get-started/install/windows#additional-windows-requirements的说法。

全部搞定后，`flutter doctor`的结果应该是这样的：

```
Flutter assets will be downloaded from https://storage.flutter-io.cn. Make sure you trust this source!
Doctor summary (to see all details, run flutter doctor -v):
[√] Flutter (Channel stable, 2.10.0, on Microsoft Windows [Version 10.0.19043.1526], locale zh-Hans-HK)
[√] Android toolchain - develop for Android devices (Android SDK version 32.0.0)
[X] Chrome - develop for the web (Cannot find Chrome executable at .\Google\Chrome\Application\chrome.exe)
    ! Cannot find Chrome. Try setting CHROME_EXECUTABLE to a Chrome executable.
[√] Visual Studio - develop for Windows (Visual Studio Community 2022 17.0.5)
[√] Android Studio (version 2021.1)
[√] VS Code (version 1.64.2)
[√] Connected device (3 available)
[!] HTTP Host Availability
    X HTTP host https://maven.google.com/ is not reachable. Reason: An error occurred while checking the HTTP host: 信号灯超时时间已到


! Doctor found issues in 2 categories.
```

大致一样就行，前 5 项除了 Chrome 以外，最好都是`[√]`。其他不用管也罢。

### 其他必须安装/配置的东西

如果你的电脑之前没有做过开发，你可能还缺少一些开发必要的软件和操作。

- [Git](https://git-scm.com/downloads)
- 如果你要连接 Android 手机，[打开 USB 调试](https://jingyan.baidu.com/article/c275f6ba71db93e33d75672b.html)

## 重要的网站

Flutter 官方中文文档：https://flutter.cn/docs/

Flutter 官方仓库：https://pub.flutter-io.cn/

Dart 语法速查：https://www.w3cschool.cn/nxvsy/

Commit 的书写规范：https://ruby-china.org/topics/15737

有问题，上Google：https://google.com/

## 第一个应用

在正式开始搞项目之前，可以先写个 Hello World 感受一下。[这里](https://flutter.cn/docs/get-started/codelab#step-1-create-the-starter-flutter-app)就有个非常详尽的手把手上手教程。

你可能没法马上搞懂所有语法细节，或者每个组件的作用，但是可以先体会体会 Flutter 的热重载和便捷的第三方库引入方式。

> **提示**
>
> 如果你编写、编译遇到了一些报错，不要恐慌，先复制粘贴搜索一下！如果尝试搜索无果，可以直接询问其他开发同学。
>
> 永远不要害怕提出问题！

## 一些与旦夕有关的东西

旦夕中使用了一些稍微有些复杂的库，是你从官方文档中读不到的。

在正式开始开发之前（**不一定是现在！**），你可能需要事先学习一下它们的用法。主要有：

- [flutter_platform_widgets](https://pub.flutter-io.cn/packages/flutter_platform_widgets)：由于 Flutter 既有针对 Material 的控件，又有针对 Cupertino 的控件，它可以用于同时给 Android 和 iOS 适配两套不同的 UI 风格；

- [provider](https://github.com/rrousselGit/provider/blob/master/resources/translations/zh-CN/README.md#%E4%BD%BF%E7%94%A8)：一个优化架构的 [InheritedWidget](https://api.flutter-io.cn/flutter/widgets/InheritedWidget-class.html) 包装。

  举个简单的例子说它的用途。如果你需要在点击一个按钮时改变某个变量，同时在另一个文本框里实时显示这个变量的值，只需要在两者的共同祖先控件上套一个`Provider`，让`Provider`持有这个变量，再让文本框从`Provider`那里获得变量并监听（`var value = context.watch<MyValueModel>().myValue`）。点击按钮时，从`Provider`那里获得变量并改变值（`context.read<MyValueModel>().myValue="123"`），这个赋值的时候就会自动刷新文本框的内容了，无需想方设法从按钮里发出通知：「文本框，你快调用`setState()`刷新一下自己！」，那样会让代码变得难以阅读。

## 接下来？

- 要快速了解 Flutter 的编写方式，从 [Flutter 的开发文档](https://flutter.cn/docs/development/ui/widgets-intro)开始。

- 第一次上手 Android Studio 这种基于 Jetbrains IDEA 的高级 IDE，总是有难度的。或许你要花上一两天时间，先把各种编辑操作的概念搞懂。如果你不喜欢重体量的 IDE，也可以试试 Visual Studio Code，它对 Flutter 的支持也不错。

- 如果对自己的水平有信心，你也可以稍后看看[旦夕的源代码](https://github.com/DanXi-Dev/DanXi/)（最初的开发者之一——@singularity 就是这么做的。他从对 Flutter 一无所知到上手 commit，只花了一两天时间），模仿着写一些简单的页面。它仍是个结构简单、很多地方偏向于**快速编写**而不是**工程性**的中等体量项目，不会有太多复杂的深奥概念，只不过第一次接触会比较陌生。放轻松！

