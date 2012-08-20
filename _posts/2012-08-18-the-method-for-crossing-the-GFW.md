---
layout: post
title: "翻墙之术"
category: 使用经验
tags: [GFW]
---
{% include JB/setup %}

## 使用目的
翻越GFW，呼吸新鲜空气

## 具体方式
要翻越GFW有多种方式，想简便的可以使用付费的VPN账号，
想免费的可以使用GAE和AWS等云应用平台自己搭建翻越GFW的中转站。
### GoAgent方式
[GoAgent](http://code.google.com/p/goagent/)也是使用GAE的方式，是使用GAE搭建的代理。
#### Mac OS X下搭建GoAgent的翻墙代理
##### 申请GAE的账号
首先需要到[GAE](http://appengine.google.com)上申请GAE账号，如果已有Gmail账号，则可以直接登陆。
##### 创建GAE应用ID
有GAE账号顺利登陆之后，就可以创建Application了，在第一次创建的时候，需要输入手机号（手机号格式为+86139xxxxxxxx形式）获取验证码来进行验证。

创建应用的过程需要输入Application的ID，Title描述等，按要求填写就可以创建成功了。一个GAE账号最多只能创建10个Application。
##### 下载GoAgent
创建好了GAE应用之后，就可以下载最新的[GoAgent](http://code.google.com/p/goagent/)稳定版，解压到你希望的目录。
##### 修改配置文件中的GAE应用ID
修改解压出来的local/proxy.ini中的[gae]下的appid=你创建的GAE应用ID（多个appid请用|隔开，如appidfirst|appidsecond|appinthird,注：用|隔开时，中间不要有空格）。
##### 上传回服务端
然后切换到上一级的server目录下，运行

		python upload.zip

命令来向GAE服务器上传，激活Application。
命令运行后，会提示输入AppID，就是GAE创建的ApplicationID，邮箱和密码就是GAE账号的邮箱和密码。
##### 启动GoAgent代理
上传成功后，返回到local目录下，运行

	python proxy.py
命令就能启动基于GAE的GoAgent代理服务。启动之后需要配置的本地代理地址为127.0.0.1，端口为8087。	

##### 使用Chrome插件
为了更加方便的解析使用代理和不使用代理直接的切换，为Chrome浏览器安装[Proxy SwitchSharp](https://chrome.google.com/webstore/detail/dpplabbmogkhghncfbfdeeokoefdjegm)插件，并且除了手动进行配置代理的地址外，也可以直接导入[SwitchyOptions.bak](http://goagent.googlecode.com/files/SwitchyOptions.bak)这个配置文件。
#### 使用FireFox插件
首先为FireFox安装GoAgent证书，FireFox->Preferences->Advanced->Encryption->View Certificates->Import,选择GoAgent的local/ca.crt证书导入，导入的时候勾选全部的Trust选项。

安装[AutoProxy](https://addons.mozilla.org/zh-CN/firefox/addon/autoproxy/)组件，安装完后重启FireFox，重启后可以按提示安装规则列表gfwlist。

为AutoProxy添加GoAgent代理，点击FireFox右上角的AutoProxy快捷下拉菜单中选择Preferences，然后点击Proxy Server中的Edit Proxy Server，添加意向GoAgent，127.0.0.1:8087。

最后在快捷下拉菜单中选择Global Mode代理模式，并且Default Proxy项选择GoAgent，就可以使用了。

FireFox中也可以选择使用[FoxyProxy](https://addons.mozilla.org/zh-cn/firefox/addon/foxyproxy-standard/)代理管理插件。

##### 使用和体验
这样安装和配置就好了，下次要使用GoAgent来翻墙的时候，先打开终端，切换到GoAgent的local目录下，使用`python proxy.py`命令打开代理，同时在Chrome浏览器中SwitchSharp插件里选择GoAgent选项，然后就可以输入[www.facebook.com](www.facebook.com)进行浏览Facebook了。

因为GAE给每个应用每天只分配了1G的流量，因此到浏览不需要翻墙就可以的网页及视频时，可以在SwitchSharp中选择Direct Connection选项不使用代理就直接连接。

### AWS方式
	


---
#### 持续更新其他的翻越GFW的方式…
