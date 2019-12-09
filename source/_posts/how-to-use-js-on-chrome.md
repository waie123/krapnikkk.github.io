---
title: how to use js on chrome
---

## 说在前面

本教程使用的是 [chrome浏览器](https://www.google.cn/intl/zh-CN/chrome/)（其他使用Chromium内核浏览器同样适用），测试网址是[百度首页](https://www.google.cn/intl/zh-CN/chrome/)，使用的测试js脚本如下：
    
```javascript
    alert("当你看到这个弹窗，说明你已经成功运行js脚本啦！");
```

## 地址栏执行

在我们要运行脚本的标签页，复制测试js脚本到地址栏，前面增加这个字符：**javascript:**
  ```javascript
  javascript:alert("当你看到这个弹窗，说明你已经成功运行js脚本啦！");
  ```
黏贴到地址栏，键盘回车，页面将运行测试js脚本

*部分高版本chrome会自动注释掉 **javascript:**,以浏览器地址栏实际显示为准，被注释掉，需要手打**javascript:**进去*

### 黏贴代码到地址栏
![0-1](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/0-1.png)

### 执行后
![0-2](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/0-2.png)

## 书签执行

使用快捷键：**Ctrl + Shift + O**，或者按照下图步骤打开**书签管理器**

### 打开书签管理器
![1-1](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/1-1.png)

进入书签管理器后，点击右上角的菜单-添加新书签

### 添加新书签
![1-2](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/1-2.png)

在弹窗中为书签添加个任意名称，其中网址就输入我们的js脚本，点击保存，保存成功后书签栏将会出现新增的书签

部分高版本浏览器保存提示*网址无效* 同样给脚本前面添加这个字符：**javascript:**就可以保存了，
  ```javascript
  javascript:alert("当你看到这个弹窗，说明你已经成功运行js脚本啦！");
  ```
### 编辑书签
![1-3](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/1-2.png)

切换到我们要运行脚本的标签页，点击书签栏的脚本即可运行脚本
【如果浏览器没有标签栏，使用快捷键**Ctrl + Shift + O**即可显示书签栏】

### 执行后
![0-2](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/0-2.png)

## 控制台执行

在我们要运行脚本的标签页，使用快捷键：**Ctrl + Shift + i**【部分浏览器可以使用快捷键**F12**】，或者按照下图步骤打开**开发者工具**

### 打开开发者工具
![2-1](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/2-1.png)

### 开发者工具界面
![2-2](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/2-2.png)

在开发者工具的**console**栏目输入我们要运行的脚本，回车执行

### 执行如下
![2-3](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/2-3.png)

小技巧：使用快捷键：**Ctrl + Shift + D**,将控制台展示调整为侧边栏，或者执行下图操作：
![2-4](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/2-4.png)

小技巧：使用快捷键：**Ctrl + Shift + M**,可以将网页模拟成移动端，或者执行下图操作：
![2-5](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/2-5.png)

## Snippets收藏和执行
参照上面的**控制台执行**方法打开开发者控制台，执行下图操作：
![3-1](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/3-1.png)

右击对应的脚本，点击*Run*运行脚本，效果如下：
![3-1](https://github.com/krapnikkk/krapnikkk.github.io/blob/master/asset/how-to-use-js-on-chrome/3-2.png)

