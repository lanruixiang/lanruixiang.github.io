---
layout: post
title: Luogu CF755B 题解
categories: Luogu
description: 原题解链接：https://www.luogu.com.cn/blog/I-like-magic/solution-cf755b
keywords: Luogu, 题解
mathjax: true
---

原题解链接：<https://www.luogu.com.cn/blog/I-like-magic/solution-cf755b>

## 分析

这题其实不难。

两人最佳的方案就是先说对方会的词。

不难证明，设先手会说 $$n$$ 个单词，后手会说 $$m$$ 个单词，

若 $$n>m$$，则先手胜，若 $$n<m$$，则后手胜。

那如果 $$n=m$$ 呢？

假设两人都会说的单词数为 $$k$$，

那么一番推理发现，当两人说了 $$k-1$$ 次，就没有两人都会的词了，可以回到之前的情况考虑。

所以，如果 $$k$$ 为奇数，$$k-1$$ 就是偶数，说完了之后两人词汇量相等，则先手胜，反之，则后手胜。

## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;
int n,m,k;
string a;
map<string,bool>f; //用于统计都会的
signed main() {
	scanf("%d%d", &n, &m);
	if(n > m) {
		puts("YES");
		exit(0);
	}else if(n < m) {
		puts("NO");
		exit(0);
	} //两种情况特殊判断
	for(int i = 1 ; i <= n ; i++){
		cin >> a;
		f[a] = 1; //统计先手会的词
	}
	for(int i = 1 ; i <= m ; i++){
		cin >> a;
		if(f[a]) k++; //统计都会的词
	}
	if(k & 1) puts("YES");
	else puts("NO"); //判断
	return 0; //完美收尾
}
```
