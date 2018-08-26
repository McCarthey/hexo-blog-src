---
title: paypal支付续订接入ccbill支付接入.md
date: 2018-06-24 23:56:22
tags:
- paypal
- curl
---

## paypal支付
- paypal一次性支付仅走express checkout即可:
  - 引入paypal/checkout.js
  - 放置需要展示的button元素（button样式定制程度较低，不可自定义css）
  - 发送请求，参数可参照payment restful接口
- paypal续订
  - 涉及到创建续订计划 -> 激活续订计划 -> 用户同意续订计划(支付) -> 创建续订
  - 以上操作均为原子操作，任何一步报错或拒绝都要返回错误

## ccbill支付
一次性支付、续订流程相同

## 支付测试
- paypal支付可使用sandbox环境（建议重新注册sandbox账号、商家账号，旧版账号登录sandbox有两个接口会报500）
- ccbill也支持sandbox环境，前提是需要登录过ccbill管理系统，然后在支付链接前缀上添加sandbox即可