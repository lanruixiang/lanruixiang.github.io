---
layout: solution
title: Luogu CF1133B 题解
categories: Luogu
description: 原题解链接：https://www.luogu.com.cn/blog/I-like-magic/cf1133b-ti-xie
keywords: Luogu, 题解
mathjax: true
---

原题解链接：<https://www.luogu.com.cn/blog/I-like-magic/cf1133b-ti-xie>。

## 分析

这道题其实很简单。

要让两数和为 $$k$$ 的倍数，需要满足以下两条件之一：

- 两数都是 $$k$$ 的倍数。

- 两数的余数和为 $$k$$。

因此，我们可以先统计出余数。

再按上述条件算出共有多少组，即可得到答案。

**注意：**

- 当 $$k$$ 为偶数时，余数为 $$\frac{k}{2}$$ 的数要两两配对，不要多算。

- 这里统计的是组数，记得输出时乘 $$2$$。

## 代码

```cpp
#include<bits/stdc++.h>//万能头文件
using namespace std;
inline int read(){
	int s = 0, w = 1; char ch =   getchar();
	while(ch < '0' || ch > '9'){ if(ch == '-') w = -1; ch = getchar(); }
    while(ch >= '0' && ch <= '9') s = s * 10 + ch - '0', ch = getchar();
    return s*w;
}
//快读
int n,k,cnt[100],sum;
int main(){
	n=read(),k=read();
	for(int i=1;i<=n;i++){
		int a=read();
		cnt[a%k]++;
	}
	sum+=cnt[0]/2;
	for(int i=1;i<k/2.0;i++) sum+=min(cnt[i],cnt[k-i]);
	if(k%2==0) sum+=cnt[k/2]/2;//余数为 k/2 的要特殊判断哦！！
	printf("%d",sum*2);//记得乘二
	return 0;//完美收尾
}
```
