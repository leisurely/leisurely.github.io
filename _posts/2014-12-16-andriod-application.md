---
layout: post
title: "安卓应用开发"
description: ""
category: 
tags: []
---
{% include JB/setup %}

#安卓开发简介
Android 是一种基于 Linux® V2.6 内核的综合操作环境。最初，Android 的部署目标是移动电话领域，包括智能电话和更廉价的翻盖手机。但是， Android 全面的计算服务和丰富的功能支持完全有能力扩展到移动电话市场以外。Android 也可以用于其他的平台和应用程序。在本文中，阅读对 Android 平台的简介，并学习如何编写基本的 Android 应用程序。

#安卓平台
Android 有丰富的功能，因此很容易与桌面操作系统混淆。Android 是一个分层的环境，构建在 Linux 内核的基础上，它包括丰富的功能。UI 子系统包括：、窗口、视图、用于显示一些常见组件（例如编辑框、列表和下拉列表）的小部件。

Android 包括一个构建在 WebKit 基础上的可嵌入浏览器，iPhone 的 Mobile Safari 浏览器同样也是以 WebKit 为基础。

Android 提供多种连接选项，包括 WiFi、蓝牙和通过蜂窝（cellular）连接的无线数据传输（例如 GPRS、EDGE 和 3G）。Android 应用程序中一项流行的技术是链接到 Google 地图，以便在应用程序中显示地址。Android 软件栈还提供对基于位置的服务（例如 GPS）和加速计的支持，不过并不是所有的 Android 设备都配备了必需的硬件。另外还有摄像支持。

过去，移动应用程序努力向桌面应用程序看齐的两个领域分别是图形/媒体和数据存储方法。Android 通过提供对 2D 和 3D 图形的内置支持，包括 OpenGL 库，解决了图形方面的挑战。由于 Android 平台包括流行的开源 SQLite 数据库，因此缓解了数据存储的负担。下图显示一个简化的 Android 软件层次结构。

<p><img src="/img/app1.gif"/></p>

应用程序架构
如前所述，Android 运行在 Linux 内核上。Android 应用程序是用 Java 编程语言编写的，它们在一个虚拟机（VM）中运行。需要注意的是，这个 VM 并非您想象中的 JVM，而是 Dalvik Virtual Machine，这是一种开源技术。每个 Android 应用程序都在 Dalvik VM 的一个实例中运行，这个实例驻留在一个由 Linux 内核管理的进程中，如下图所示。

<p><img src="/img/app2.gif"/></p>

Android 应用程序由一个或多个组件组成：

活动 具有可视 UI 的应用程序是用活动实现的。当用户从主屏幕或应用程序启动器选择一个应用程序时，就会开始一个动作。

服务 服务应该用于任何需要持续较长时间的应用程序，例如网络监视器或更新检查应用程序。

内容提供程序 可以将内容提供程序看作数据库服务器。内容提供程序的任务是管理对持久数据的访问，例如 SQLite 数据库。如果应用程序非常简单，那么可能不需要创建内容提供程序。如果要构建一个较大的应用程序，或者构建需要为多个活动或应用程序提供数据的应用程序，那么可以使用内容提供程序实现数据访问。

广播接收器 Android 应用程序可用于处理一个数据元素，或者对一个事件（例如接收文本消息）做出响应。

Android 应用程序是连同一个 AndroidManifest.xml 文件一起部署到设备的。AndroidManifest.xml 包含必要的配置信息，以便将它适当地安装到设备。它包括必需的类名和应用程序能够处理的事件类型，以及运行应用程序所需的许可。例如，如果应用程序需要访问网络 — 例如为了下载一个文件 — 那么 manifest 文件中必须显式地列出该许可。很多应用程序可能启用了这个特定的许可。这种声明式安全性有助于减少恶意应用程序损害设备的可能性。

#安卓开发环境搭建
安卓应用开发环境详见<a href="http://blog.sina.com.cn/s/blog_4de067e40100mnl7.html">搭建Android应用开发环境</a>

#helloworld应用
本节展示如何构建一个 Android 应用程序。示例应用程序非常简单：一个修改后的 “Hello world” 应用程序，并稍加改动。

在 Eclipse 中创建应用程序，选择 File > New > Android project，这将启动 New Android Project 向导。

<p><img src="/img/app3.jpg"/></p>

接下来，创建一个简单的应用程序，该应用程序有一个活动，并且在 main.xml 中有一个 UI 布局。布局包含一个文本元素，您将修改这个文本元素，以显示 Android FlashLight。下面的清单显示了这个简单的布局。这是应用的主界面的控件布局（位置）。

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
		android:orientation="vertical"
		android:layout_width="fill_parent"
		android:layout_height="fill_parent"
		android:background="@color/all_white">
	<TextView  
		android:layout_width="fill_parent" 
		android:layout_height="wrap_content" 
		android:text="@string/hello" android:textColor="@color/all_black" 
	   android:gravity="center_horizontal"/>
	</LinearLayout>
	
在 strings.xml 中创建两个颜色资源，该文件为一些资源的定义相当于c语言中的宏定义。

	<?xml version="1.0" encoding="utf-8"?>
	<resources>
		<string name="hello">Hello World！</string>
		<string name="app_name">Helloworld</string>
		<color name="all_white">#FFFFFF</color>
		<color name="all_black">#000000</color>
	</resources>

主屏幕布局有一个定义为 all_white 的背景色。在 strings.xml 文件中，可以看到 all_white 被定义为一个值为 #FFFFFF 的 RGB 三元组，即纯白。

布局包含一个 TextView，这实际上是一块静态文本。它是不可编辑的。文本被设为黑色，并通过 gravity 属性设为水平居中。

该应用程序有一个名为 Helloworld.java 的 Java 源文件，如以下清单所示。

	package com.msi.Helloworld;
	import android.app.Activity;
	import android.os.Bundle;
	public class Helloworld extends Activity {
		/** Called when the activity is first created. */
		public void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			setContentView(R.layout.main);
		}
	}
	
该代码是直接来自 New Project 向导的模板代码：

它是 Java 包 com.msi.Helloworld 的一部分。

它有两个 import：

一个用于 activity 类

一个用于 bundle 类

当该活动发起后，onCreate 方法被调用，传入一个 savedInstanceState。对于我们来说，不必关心这个 bundle。只有在暂停然后恢复活动时才会用到。

onCreate 方法覆盖了同名的 activity 类方法。它调用超类的 onCreate 方法。

对 setContentView() 的调用将关联 main.xml 文件中定义的 UI 布局。main.xml 和 strings.xml 中的任何内容都自动映射到 R.java 源文件中定义的常量。任何时候都不要直接编辑这个文件，因为它随着每次构建而改变。

运行该应用程序可以看到一个白色屏幕，其中有黑色文本Helloworld。