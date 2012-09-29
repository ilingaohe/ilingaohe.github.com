---
layout: post
title: "iOS Event Handling"
caterogy: 学习笔记
tags: [iOS EventHandle]
---
{% include JB/setup %}

## 学习目的
客户端程序中需要和用户的交互，而如果要在程序中对用户的点击等事件进行有效响应，就需要了解下iOS的Event Handling处理。
## 具体内容
### 事件类型
iOS系统中有三种类型的事件，Touch，Motion和RemoteControl：

	typedef enum {
    	UIEventTypeTouches,
    	UIEventTypeMotion,
    	UIEventTypeRemoteControl,
	} UIEventType;
	
其中每种类型又有子类型：

	typedef enum {
    	UIEventSubtypeNone                              = 0,
 
    	UIEventSubtypeMotionShake                       = 1,
 
    	UIEventSubtypeRemoteControlPlay                 = 100,
    	UIEventSubtypeRemoteControlPause                = 101,
    	UIEventSubtypeRemoteControlStop                 = 102,
    	UIEventSubtypeRemoteControlTogglePlayPause      = 103,
    	UIEventSubtypeRemoteControlNextTrack            = 104,
    	UIEventSubtypeRemoteControlPreviousTrack        = 105,
    	UIEventSubtypeRemoteControlBeginSeekingBackward = 106,
    	UIEventSubtypeRemoteControlEndSeekingBackward   = 107,
    	UIEventSubtypeRemoteControlBeginSeekingForward  = 108,
    	UIEventSubtypeRemoteControlEndSeekingForward    = 109,
	} UIEventSubtype;
	
		
### 事件传递