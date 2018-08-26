---
title: 基于Vue-cli的PWA升级
date: 2018-06-17 16:38:04
tags: 
- vue
- PWA
---

webpack核心插件：[offline-plugin](https://www.npmjs.com/package/offline-plugin) ,[sw-precache-webpack-plugin](https://www.npmjs.com/package/sw-precache-webpack-plugin)

# 升级过程
PWA相关知识在此不再赘述，之前的文章也提到过一些。我们主要需要manifest.json和service-worker.js。由于项目[loveblock]静态资源过多（图片+css+js共50+个请求），因此在service-worker的中需要拦截这些资源请求。

插件的接入过程可参考插件的官方文档，写得很详细。在此仅叙述升级过程中遇到的问题:

### 1.与七牛CDN结合使用
一开始我使用的是[offline-plugin插件](https://www.npmjs.com/package/offline-plugin)，简单好用，但是控制台一直会报错，排查后发现是因为插件默认把service-worker的注册逻辑打包到了js中并上传到CDN，导致service-worker无法通过外部脚本注册

### 2.缓存html文件
为解决上述问题，我换用了[sw-precache-webpack-plugin插件](https://www.npmjs.com/package/sw-precache-webpack-plugin)。这个插件就不存在上述问题，因为service-worker的注册是要我们手动完成的。因此，可以将以下代码添加进模板中（官方实例）:
```javascript
(function() {
  if('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/service-worker.js');
  }
})();
```
打包后会发现新生成了service-worker.js，里面有我们想要缓存的资源。我们发现资源缓存数组中的第一个元素就是XXXX.html，即是我们的html文件。
（未完待续）

