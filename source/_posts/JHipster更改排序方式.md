---
title: JHipster更改排序方式
date: 2018-08-12 21:47:30
tags: angular
categories: JHipster
---

## 需要修改的代码

在*.route.ts文件中（比如user-management.route.ts）找到如下代码：
```
const sort = route.queryParams['sort'] ? route.queryParams['sort'] : 'id,asc';
```

## 更改代码
将上述文件更改为：
```
const sort = route.queryParams['sort'] ? route.queryParams['sort'] : 'id,desc'
```
## 描述
Jhipster默认采用根据id升序排序，但一般会采用降序排序，如果希望全部修改，可以使用ide全局搜索关键词：id,asc，改为id,desc，即可全部更改。