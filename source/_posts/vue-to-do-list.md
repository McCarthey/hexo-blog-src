---
layout: post
title: vue实践（二）———— VueToDoList
date: 2018-05-14 23:53:47
tags:
- vue
- webpack
---

还记得我的那个原生 js 写的 to-do-list 吗？原 demo 地址=>[A-To-do-list](https://mccarthey.github.io/A-To-do-list)
这次使用 vue 来实现，demo 地址=>[Vue-To-do-list](https://mccarthey.github.io/VueToDoList/)

# 项目简介

为了解决上一个[to-do-list](https://mccarthey.github.io/A-To-do-list)应用原生 js 操作 DOM 而引起的网页性能问题，也是为了向一个[Freelancer](https://www.freelancer.cn)上认识的日本小哥介绍一下 Vue 这个框架，决定写一个 Vue 版本的 todolist 来说明。

# 编程实现

不多说，先上代码，仓库地址=>[VueToDoList](https://github.com/McCarthey/VueToDoList)。

整个代码库很简单，因为是使用 vue-cli 的 webpack-simple 模板构建的，因此几乎没有配置修改的余地（毕竟只是一个小应用，也没涉及到代理、接口）。代码基本都写在 App.vue 中。

* 列表渲染模板

```html
    <draggable v-model="myArray" @end="onDrop">
        <!-- transition/animation https://vuefe.cn/v2/guide/transitions.html -->
      <transition-group name="list">
        <div v-for="(element,index) in myArray" :key="index" class="draggable-item">
        <!-- A material design UI library for Vue.js, museUI  https://www.muse-ui.org -->
          <mu-checkbox class="checkbox" v-model="element.done"/>
          <mu-text-field v-model="element.text" hintText="写点儿什么吧" @blur="onSave" :disabled="element.done" :class="element.done? 'act-input-done': 'act-input' " />
          <mu-icon-button icon="delete" @click="onDelete(index)" iconClass="icon-delete"/>
          <!-- 是否需要多行文本 -->
        </div>
      </transition-group>
    </draggable>
```

其中`v-for`循环渲染的`div`元素外层包裹了`<transition-group>`，用于展示元素的过渡动画（[可参考 vue 的官方文档](https://vuefe.cn/v2/guide/transitions.html#%E5%88%97%E8%A1%A8%E8%BF%87%E6%B8%A1)），因此这是可选的。而`<transition-group>`的外层又包裹了`<draggable>`元素，这里可参考[vuedraggable 的官方文档](https://www.npmjs.com/package/vuedraggable)。引入 vuedraggable 后列表元素就变成了可拖拽的，而不仅仅是之前版本的置顶操作（PS：其实这个需求是应女票要求加上的，没错，她是我这个小应用的忠实用户 :D ）。

* 操作按钮

```html
    <div class="op-btn_group">
      <div class="op-btn_group-left">
        <mu-raised-button label="新建" class="raised-button btn-new" backgroundColor="#4caf50" @click="onCreate"/>
      </div>
      <div class="op-btn_group-right">
        <mu-raised-button label="保存" class="raised-button btn-save" @click="onSave" primary/>
        <mu-raised-button label="清空" class="raised-button btn-delete" @click="onClearAll" secondary/>
      </div>
    </div>
```

然后是三个功能按钮，分别触发三种不同的事件:

1.  新建事件：在列表数组尾部添加一个对象元素
2.  保存事件：将列表数组 JSON 字符串化，存入到 localStorage 中（键名依然是'mc_to_do_list'，数据的迁移下文会讲）
3.  清空事件：弹出提示框，确认清空所有事件（删除 localStorage 中键名是'mc_to_do_list'的值）

由于代码比较简单，就不贴出了，请直接在代码库里查看

* 老数据迁移
