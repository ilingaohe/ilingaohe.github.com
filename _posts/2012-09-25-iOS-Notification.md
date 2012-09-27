---
layout: post
title: "iOS Notification学习"
caterogy: 学习笔记
tags: [iOS NSNotification]
---
{% include JB/setup %}

## 学习目的
iOS中的NSNotification方式提供了一种松耦合的消息传递机制。
## 具体内容
### NSNotificationCenter
同步发送消息，只有各个Observer都接收了消息并return返回，才继续执行。
### NSNotificationQueue
把NSNotification放入Queue中，然后就立即返回，由Queue再负责在合适的时机把消息投递给NSNotificationCenter，从而实现异步发送消息。
### NSNotification与线程
NSNotificationCenter只会把NSNotification发送给post时所在的那个线程。
如果需要发送给其他的线程进行处理，需要额外的处理。