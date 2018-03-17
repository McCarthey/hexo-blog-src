---
layout: post
title: 可以本地存储的to-do list
date: 2017-06-14 11:47:46
tags: 
- to-do-list
- localStorage
- PWA
---
一个to-do list也要玩花样？没错，没有存储功能的to-do list几乎没有实用价值。
demo地址=>[A-To-do-list](https://mccarthey.github.io/A-To-do-list)
# localStorage简介
  cookie一直都是Web开发人员用来存储数据的有效工具，但是cookie存在的一些问题限制了它的应用范围：
	* 读取cookie需要冗余的代码
	* cookie是HTTP的功能而不是浏览器的
	* 浏览器限制了cookie的数量和大小(4KB)
	* cookie会过期
  因此HTML5引入了Web存储功能--本地存储(localStorage)和会话存储(sessionStorage)。localStorage具有以下优点：
  	* 开发人员可以方便地设置、写入数据和读取数据
  	* 拥有5MB(IE中有10MB)的超大存储空间
  	* localStorage中的数据不会过期，永远有效，除非手动删除
  	* 键/值对的存储方式，简单方便
  具体使用方法可以参考[HTML5 Web存储](http://www.w3school.com.cn/html5/html_5_webstorage.asp)，保证5分钟内就能学会XD。
# 编程实现
  因为只是个很小的应用，所以我并未引用任何第三方库，都是用原生js来操作dom实现的，好处是文件都很小，不会出现几百k的怪物库；弊端就是操作dom频繁，性能会受到影响，但是影响不大。
  主要实现的功能：
  	* 新建事项
  	* 标记事项为完成/未完成状态
  	* 删除某事项
  	* 清空全部事项
  	* 事项置顶
  	* 动画优化
  	* 移动端优化
  具体的代码可以到github库中查看下载[A-To-do-list Github](https://github.com/McCarthey/A-To-do-list)
# 改造成PWA
  因为它是一个github page应用，在有网络的条件下可以随时访问。但是有些应用场景网络连接受限不畅通，或者是使用者忘记打开移动数据等，这些问题都会导致用户无法使用或者体验不佳。因此我将其升级成了PWA，使得用户可以将其放入手机主屏，而不用打开浏览器输入烦人的url，同时使其离线可访问(因为数据都是存放在浏览器的localStorage中，无需网络即可写入、读取)。
# 存在的问题
  未对用户输入做过滤，会收到XSS攻击(未来会补充)