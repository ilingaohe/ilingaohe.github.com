---
layout: post
title: "iOS Reveal Side View开源实现学习"
category: 学习笔记
tags: [iOS UI OpenSource]
---
{% include JB/setup %}

## 学习目的
苹果在iOS上提供了很多很有特色的UI实现，包括很好用的UINavigationController，UITabBarController等等各种UI容器，使用苹果提供的UI已经可以实现很好的应用了。但是应用想要有自己与众不同的特点，就需要自定义自己的UI结构，比如Path的左右可以显示和隐藏的侧边栏UI结构，就很与众不同与吸引眼球。因此网上也出现了模仿这种UI效果的开源实现，这里学习几个比较好的开源实现，学习他们的思路，比较他们的不同，并用到以后自己写自定义UI结构的思路中。
## 具体内容
Github上现在有多个Reveal Side View的实现，这里主要来学习下[JASidePanels](https://github.com/gotosleep/JASidePanels/tree/)，[JTRevealSidebarDemo](https://github.com/mystcolor/JTRevealSidebarDemo)和[ZUUIRevealController](https://github.com/pkluz/ZUUIRevealController)这三个的实现。
### JASidePanels
