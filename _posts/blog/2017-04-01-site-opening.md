---
layout: post
title:  我的个人主页开！站！了！
category: blog
description: 利用gitpage+jekyll，倒腾了两天
---

##1. 为啥要建站
之前有过在新浪和QQ空间写博客的经历，但是对那些恶俗的模版和花里胡哨功能十分之反感，因此2017年的计划里就给自己增加了一项：建设一个自己的网站。
这件事情其实从去年就开始筹划，先买了域名，然后打算在amazon上承包个主机，用flask+python弄起来。本人作为产品狗，对前端coding自然有些了解，但是让我从头写html，js，css，还部署到云（甚至当时想到了docker）里，时间成本和学习成本还是挺高的。
前两天有个很偶然的机会了解到gitpage这个东西，快速的模版继承和代码托管让我眼前一亮！就它了！

##2. 环境准备
选择了方案，就开始进行环境准备。
基于成本最小化考虑，选择了办公pc上的windows，哈哈，我有够懒吧。
基本过程就是先装ruby和gem（因为jekyll是用ruby编写的），然后安装jekyll和其依赖的各种package。
具体可以参考：
<http://pwnny.cn/original/2016/06/26/MakeBlog.html>

整个过程产生了不少问题，主要需要注意几点：

1. 要翻墙
2. 安装完ruby和gem后，还需要把ruby的devkit装好
3. 在本地测试jekyll的时候，新版本(3.3以后)生成的目录结构和官网上是不一样的，主要是缺少include和layout这两个文件夹。这个问题一度让我无法继续，在jekyll的官网上找到了答案如下:

> Starting Jekyll 3.2, a new Jekyll project bootstrapped with jekyll new uses gem-based themes to define the look of the site. This results in a lighter default directory structure : _layouts, _includes and _sass are stored in the theme-gem, by default.
minima is the current default theme, and bundle show minima will show you where minima theme's files are stored on your computer.

所以就用anything搜索了下minima，顺利找到然后拷贝出来即可。

4. 碰到问题一定看官方spec，按顺便来，一定能解决问题

##3. 选择模版
之前说道jekyll最大的好处是和github的深度集成，模版继承和代码托管，不要太方便（和便宜）
在github里搜了几个心仪的模版然后folk一下到本地，修改部分代码，再submit到自己的github项目里，done！
这个过程比较顺利，主要需要注意几点：

1. 在使用一个模版前最好先弄清楚它依赖哪些package，因为有可能你的主页使用了该模版后，无法在github上build出来
2. github提供了几种markdown解释器，在jekyll的_config.yml里可以修改，尽量选用对中英文都兼容较好的，我选的rdiscount（其实是我模版作者选的，羞愧脸，经我验证确实不错）

##4. 写文章
按照markdown语法写好文章，就可以上传到posts目录里了。
这里不禁要吐槽一下markdown的语法，不同的网站支持的居然都不太一样。我从简书上拿下来的文章，就无法被rdiscount正常解析。
gitpage需要遵守的语法规则可以参考下面链接：
<http://blog.leanote.com/post/freewalk/Markdown-%E8%AF%AD%E6%B3%95%E6%89%8B%E5%86%8C#title-9>

##5. 尽情享受创作的乐（装）趣（逼）吧
over
