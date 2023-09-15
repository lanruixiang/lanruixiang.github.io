---
layout: post
title: 随机链接
categories: OI
description: 随机洛谷用户链接
keywords: Luogu, OI, 随机, HTML
mathjax: true
---

此链接随机地指向一个洛谷 uid 小于等于 1000000 的用户：

<script language="javascript">
var a=parseInt(Math.random()*1000000);
document.write("<a href=\"https://www.luogu.com.cn/user/",a,"\">","Link","</a>");
</script>

---

此链接随机地指向一个洛谷编号小于等于 600000 的帖子：

<script language="javascript">
var a=parseInt(Math.random()*600000);
document.write("<a href=\"https://www.luogu.com.cn/discuss/",a,"\">","Link","</a>");
</script>

---

此链接随机地指向一个洛谷 P 题库中小于 P9617 的题目：

<script language="javascript">
var a=parseInt((Math.random()*8617)+1000);
document.write("<a href=\"https://www.luogu.com.cn/problem/P",a,"\">","Link","</a>");
</script>