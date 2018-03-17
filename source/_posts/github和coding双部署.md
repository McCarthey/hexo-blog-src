---
layout: post
title: github和coding双部署
date: 2017-08-16 16:39:00
tags:
- github
- coding
- blog
---
github pages太慢？不打紧，国内用coding.net托管就好啦

# coding托管
[coding](https://coding.net/) 和github一样，也是基于git的代码托管网站。
相比于github，在国内coding的访问、部署速度都要快一些，而且可以免费创建私人代码库哦。

我们的免费静态blog通常都是使用github pages搭建，套上各种炫酷的hexo主题(强烈推荐 [Material](https://material.viosey.com/) 主题，国人老铁做的，尽享MD设计之美)，或是使用 [Jekyll](https://jekyllrb.com/) 生成。搭建出来的博客效果很好，除了一个致命的缺点，**慢！**在国内访问我们的站点真的是巨慢，即使是把静态资源放到CDN上，也还是慢。慢到什么程度，放张图感受下：

![github pages](/img/post/coding.net/github page.png)

页面完全载入需要40多秒......不过也可能是我的主题静态资源太多导致的时间过长。

现在让我们把项目托管到 [coding.net](https://coding.net/) 上，注册帐号=>创建仓库=>启用pages服务=>部署公钥这些步骤就不细细说明了，和github上面的操作大体相同。
我们只需要修改一下hexo主目录下的配置文件_config.yml就好了，即添加上coding的代码库地址，
```
  type: git
  repository:
    github: git@github.com:XXXXX/XXXX.github.io.git
    coding: git@git.coding.net:XXXX/XXXX.git
```
这样我们每次deploy的时候就会同时更新github和coding的代码库，使之同步。

现在让我们来看一看打开coding pages的速度吧：

![coding pages](/img/post/coding.net/coding page.png)

页面完全载入的时间大约是github page的1/30......(虽然我不知道为什么资源请求数比github.io的少了那么多)
要知道
> 用户多等100ms,流失率增加1% 

你算算我们提速后可以多挽留住多少用户啊(答案是0，因为我们的站点根本就没有被百度、google收录LOL)
