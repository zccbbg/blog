---
title: JPA Query 处理为 NULL 的参数
date: 2018-10-25 20:37:12
tags:
- JPA
- Query
categories: JPA
---

# 问题描述
当你有很多参数作为查询条件，并且这些参数可能为null，如下代码：
```java
@Query(value = "SELECT ord.purchaseOrderNumber,ord.salesOrderNumber,ord.quoteNumber"

            + " FROM Order ord WHERE ord.purchaseOrderNumber LIKE :poNumber%  "
            + " AND ord.salesOrderNumber LIKE :soNumber "
            + " AND ord.quoteNumber = :quoteNumber "

```
当参数:quoteNumber为null时，我们该如何处理？

# 解决方案

我们可以增加一些判定条件就可以解决这个问题， eg：
> + " AND (ord.quoteNumber = :quoteNumber or :quoteNumber is null or :quoteNumber = '' ")
