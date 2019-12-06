---
title: 快人一步，招商掌上生活活动篇
date: 2019-10-03 17:44:18
tags: 
    - 快人一步
    - 兴趣使然
---

前段时间公司旅游去了一趟马来西亚，发现掌上生活有个[【非常全球 刷新世界】](https://market.cmbchina.com/ccard/wap/201909fcqqapp/index.html)，境外刷卡先刷后返现活动，回血新技能~

但是！这个活动名额很少！每天就350个名额，而且秒无。可以想象这大概也是个境外灰产套现好路子~
身为程序猿接受挑战！
<!--more-->
## 让APP变得可以调试网页
### 工具一览：windows + 小米note2 + magisk + xposed + chrome 
明眼一看就知道这是个网页，但是要怎么调试这个网页呢，浏览器打开活动页，直接跳转到cmblife:协议开头的路径，app上的表现就是一个授权登录的过程，那我们用chorme浏览器inspect查看网页源码（需要梯子），发现webview关闭了debug，幸好我还是个酷安搞基达人，知道Xposed有个WebViewDebugHook模块，说干就干，掏出备用机小米note2折腾了一下装了个magisk，安装了xposed框架，再装了个WebViewDebugHook模块，搞定~
![img](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/quick-cmbchina-activity/WebViewDebugHook.jpg?raw=true)
具体可参考这篇文章：
https://www.cnblogs.com/wmhuang/p/7396150.html

## 调试网页
活动未开始前，【立即抢】按钮是无法点击的，这个简单，我们通过调试【立即抢】按钮的dom发现这个方法

`seckillHome.receivePrize(good.goodsId， campaign.campaignNo， campaign.title)`
![img](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/quick-cmbchina-activity/00_btn_receivePrize.png?raw=true)

全局搜索找到receivePrize方法，通过阅读代码，我们发现 vm.isBtnActive 这个方法影响了AXIO【aixos喵喵喵？】请求调用，这里断一下点，手机点击一下【立即抢】按钮，跑进断点里面，手动改一下vm.isBtnActive方法

`vm.isBtnActive = function(){return true;}`

![img](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/quick-cmbchina-activity/01_receivePrize.png?raw=true)

然后代码就跑进了正常开始领取环节,手机弹窗提示活动木有开始，按钮也变成可以点击状态，而且木有发现任何http请求，王德发，多半是iframe载入了。。。

继续往下阅读代码发现了提交数据的 AXIO.post4Data 方法，在这个方法调用的时候断点，点击一下【立即抢】按钮进入断点，调试输入这个方法，看看这个方法是从哪里声明的（鼠标点击调试控制台的函数详情即可跳转到对应的声明出处）~
![img](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/quick-cmbchina-activity/02_post4Data.png?raw=true)

找到AXIO模块和post4Data方法，最后发现提交的参数通过一连串的包装后，通过 UTIL.executeProtocol(href) 方法发送请求，UTIL.executeProtocol方法通过上面同样调试输入的方法，发现是一个简单的插入iframe再自动移除的方法
![img](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/quick-cmbchina-activity/03_executeProtocol.png?raw=true)

然后瞄瞄href这个参数是什么东西，encodeURIComponent解码一下

`cmblife://web/post/cpSeckill/seckill.json?callback=javascript:receivePrizeCallback&params={"cgName":"fcqq201909","campaignNo":"48ac7fcc000c466cac2720d201e0af94","goodsId":"47916","confirmCheck":"1"}&timeout=10`

手动调用一下，发现报错了，提示receivePrizeCallback这个方法未定义，到这里可以知道iframe载入的是一种类似jsonp的机制，callback就是请求回来iframe里面的方法，手动写一下这个方法
![img](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/quick-cmbchina-activity/04_href.png?raw=true)
`function receivePrizeCallback(data){
	var res = decodeURIComponent(data);
	console.log(res);
}`

ojbk~我们这样子就可以快人一步，在活动还没有开始的时候提交请求了~

![img](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/quick-cmbchina-activity/05_code.png?raw=true)

具体代码如下：

`function executeProtocol(){		
	var iframe = document.createElement("iframe");
	iframe.style.cssText = "display:none;width:0px;height:0px;",
	iframe.src = "cmblife://web/post/cpSeckill/seckill.json?callback=javascript%3AreceivePrizeCallback&params=%7B%22cgName%22%3A%22zhoumobanjia20191001%22%2C%22campaignNo%22%3A%2286fcd88e53214822b494fd90867db853%22%2C%22goodsId%22%3A%2249657%22%2C%22confirmCheck%22%3A%221%22%7D&timeout=10",
	(document.body || document.documentElement).appendChild(iframe),
	setTimeout(function() {
		iframe && iframe.parentNode && iframe.parentNode.removeChild(iframe)
	}, 0)
}

function receivePrizeCallback(data){
	var res = decodeURIComponent(data);
	console.log(res);
}`

### 写在最后
发现招商掌上生活的所有活动都是这样，比如半价电影票，各种积分兑换之类的~






