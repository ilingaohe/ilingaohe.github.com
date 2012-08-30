---
layout: post
title: "iOS未使用ARC的内存管理"
category: 学习笔记
tags: [iOS]
---
{% include JB/setup %}

## 学习目的
学习iOS使用引用计数的内存管理方式。

## 具体内容
最近在看[《Pro Multithreading and Memory Management￼for iOS and OS X》](http://www.amazon.com/Pro-Multithreading-Memory-Management-iOS/dp/1430241160)，这本书主要介绍了iOS和Mac OS X平台上的内存管理和多线程技术。
其中内存管理在介绍了使用ARC前的引用计数方式后，主要介绍了ARC方式内存管理的实现和使用。

多线程技术主要介绍了用来方便实现多线程的Block和GCD的实现和使用。

刚看了第一章《iOS在ARC前的内存管理》，感觉对较深入的理解iOS的引用计数方式内存管理的实现还是很有帮助的，因此顺便以重点翻译和自己理解的方式记录下学习笔记。

### iOS的内存管理技术
iOS在提供ARC（Automatic Reference Counting）之前，使用的引用计数的内存管理方式。
为了理解引用计数的概率，作者以一个房间中灯泡的开关为例进行了很到位的讲解。

![使用房间的灯泡开关来比较引用计数方式的内存管理](https://raw.github.com/ilingaohe/ilingaohe.github.com/master/_posts/images/2012-08-17-01.png)

图-1 使用房间的灯泡开关来比较引用计数方式的内存管理

图-1表示对房间中的人进行计数，计数值初始为0，当新进来一个人的话，计数值就加1，离开一个人的话，计数值减1，因此当计数值大于0就表示房间中有人，灯的状态为需要为开。当计数值为0就表示房间没有人，灯就可以关掉。


