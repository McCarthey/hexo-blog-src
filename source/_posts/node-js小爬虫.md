---
title: node.js小爬虫
date: 2017-10-13 22:28:06
tags:
- node.js
- 爬虫
---

福利福利！用 node.js 爬[煎蛋](http://jandan.net/ooxx)妹子图！一行命令，百张妹图 LOL

github 地址=>[传送门](https://github.com/McCarthey/jandan-spider)

（需安装好[node.js](https://nodejs.org/en/download/)）使用很简单，把文件 git clone 下来后，cd 到该目录，输入 node first-spider 命令运行程序，然后就等着看 image 文件夹下的嘿嘿嘿吧

核心代码是利用[cheerio](https://www.npmjs.com/package/cheerio)来解析 html，如下所示

```javascript
let $ = cheerio.load(html);
for (let i = 0; i < imgMax; i++) {
  let img = $('#comments .text img').eq(i);
  ...
}
```

将`cheerio.load(html)`赋值给`$`，这样使用起来就像是 jQuery 的操作符，而且选择器使用起来也和 jQuery 十分相似，很容易使用。

需要注意，程序默认爬 10 页，每页 10 张图。可以修改全局变量 pageMax，imgMax 来控制数量。

（目前程序并没有控制请求的数量，如果请求的频次太高可能会被目标网站 ban……）
