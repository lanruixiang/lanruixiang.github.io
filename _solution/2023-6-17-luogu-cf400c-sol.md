---
layout: solution
title: Luogu CF400C 题解
categories: Luogu
description: 原题解链接：https://www.luogu.com.cn/blog/I-like-magic/solution-cf400c
keywords: Luogu, 题解
mathjax: true
---

原题解链接：<https://www.luogu.com.cn/blog/I-like-magic/solution-cf400c>

## 分析

这道题其实不难，只是一道非常简单的模拟题。

我们发现，每顺时针转动 $$4$$ 次、镜面对称 $$2$$ 次、逆时针旋转 $$4$$ 次，就变回原来的样子了。

所以，在操作前，我们可以让 $$x$$ 变成 $$x\bmod 4$$，$$y$$ 变成 $$y\bmod 2$$，$$z$$ 变成 $$z\bmod 4$$。

接下来，只需在草稿纸上画一画，即可知道顺时针转一次，一个点的 $$x$$ 值会变为原来的 $$y$$ 值，$$y$$ 值会变为原来的 $$n-x+1$$ 的值；镜面对称一次，一个点的 $$y$$ 值会变为原来的 $$m-y+1$$ 的值；逆时针转一次，一个点的 $$y$$ 值会变为原来的 $$x$$ 值，$$x$$ 值会变为原来的 $$m-y+1$$ 的值。要注意，两个旋转操作后要交换 $$n$$ 和 $$m$$。

---

This problem is not difficult, it's just a very simple simulation problem.

We found that every $$4$$ clockwise rotations, $$2$$ mirror symmetry rotations, and $$4$$ counterclockwise rotations, it returns to its original state.

So, before proceeding, we can set $$x\to x \bmod 4$$, $$y \to y \bmod 2$$, and $$z \to z \bmod 4$$.

Next, just draw a picture on the draft paper to know that if you turn it clockwise once, the $$x$$ value of a point will become the original $$y$$ value, and the $$y$$ value will become the original $$n-x+1$$ value; Once the mirror is symmetrical, the $$y$$ value of a point will change to the original $$m-y+1$$ value; Rotate counterclockwise once, and the $$y$$ value of a point will become the original $$x$$ value, and the $$x$$ value will become the original $$m-y+1$$ value. Note that after two rotation operations, $$n$$ and $$m$$ need to be swapped.

## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;
int n,m,x,y,z,p;
struct e{
	int x,y;
}d[100005];
void fun1(int t){
	while(t--){
		for(int i=1;i<=p;i++){
			int o=d[i].x;
			d[i].x=d[i].y;
			d[i].y=n-o+1;
		}
		swap(n,m); //记得交换
	}
}
void fun2(int t){
	while(t--){
		for(int i=1;i<=p;i++){
			d[i].y=m-d[i].y+1;
		}
	}
}
void fun3(int t){
	while(t--){
		for(int i=1;i<=p;i++){
			int o=d[i].y;
			d[i].y=d[i].x;
			d[i].x=m-o+1;
		}
		swap(n,m);
	}
}
int main(){
	cin>>n>>m>>x>>y>>z>>p;
	x%=4;y%=2;z%=4; //记得模一下
	for(int i=1;i<=p;i++)cin>>d[i].x>>d[i].y;
	fun1(x);fun2(y);fun3(z);
	for(int i=1;i<=p;i++)cout<<d[i].x<<" "<<d[i].y<<"\n";
	return 0;
} 
```
