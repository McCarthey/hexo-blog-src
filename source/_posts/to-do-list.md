---
layout: post
title: 可以本地存储的to-do list
date: 2017-06-14 11:47:46
tags: 
- to-do-list
- localStorage
- PWA
---

一个 to-do list 也要玩花样？没错，没有存储功能的 to-do list 几乎没有实用价值。
demo 地址=>[A-To-do-list](https://mccarthey.github.io/A-To-do-list)

# localStorage 简介

cookie 一直都是 Web 开发人员用来存储数据的有效工具，但是 cookie 存在的一些问题限制了它的应用范围：
_ 读取 cookie 需要冗余的代码
_ cookie 是 HTTP 的功能而不是浏览器的
_ 浏览器限制了 cookie 的数量和大小(4KB)
_ cookie 会过期
因此 HTML5 引入了 Web 存储功能--本地存储(localStorage)和会话存储(sessionStorage)。localStorage 具有以下优点：
_ 开发人员可以方便地设置、写入数据和读取数据
_ 拥有 5MB(IE 中有 10MB)的超大存储空间
_ localStorage 中的数据不会过期，永远有效，除非手动删除
_ 键/值对的存储方式，简单方便
具体使用方法可以参考[HTML5 Web 存储](http://www.w3school.com.cn/html5/html_5_webstorage.asp)，保证 5 分钟内就能学会 XD。

# 编程实现

因为只是个很小的应用，所以我并未引用任何第三方库，都是用原生 js 来操作 dom 实现的，好处是文件都很小，不会出现几百 k 的怪物库；弊端就是操作 dom 频繁，性能会受到影响，但是影响不大。
主要实现的功能：
_ 新建事项
_ 标记事项为完成/未完成状态
_ 删除某事项
_ 清空全部事项
_ 事项置顶
_ 动画优化 \* 移动端优化
具体的代码可以到 github 库中查看下载[A-To-do-list Github](https://github.com/McCarthey/A-To-do-list)

# 改造成 PWA

因为它是一个 github page 应用，在有网络的条件下可以随时访问。但是有些应用场景网络连接受限不畅通，或者是使用者忘记打开移动数据等，这些问题都会导致用户无法使用或者体验不佳。因此我将其升级成了 PWA，使得用户可以将其放入手机主屏，而不用打开浏览器输入烦人的 url，同时使其离线可访问(因为数据都是存放在浏览器的 localStorage 中，无需网络即可写入、读取)。

# 存在的问题

未对用户输入做过滤，会收到 XSS 攻击(未来会补充)
