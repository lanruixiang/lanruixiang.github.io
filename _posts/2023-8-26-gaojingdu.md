---
layout: post
title: 高精度模版
categories: OI
description: 高精度模版
keywords: OI, 高精度
mathjax: true
---

以下是我写的高精度模版

> 写的比较垃圾

## 使用说明

- `BigInt` 高精度结构体
  - `len` 高精度数的长度
  - `f` 负数标记
  - `a[]` 高精度数组
  - `void clear()` 清空
  - `void scan()` 读入
  - `void print(char c)` 输出，并以参数 `c` 结尾，如果 `c` 为 `?` 则不输出任何字符
  - `void dzero()` 删除前导零
  - `void chzero()` 把 $$-0$$ 变成 $$0$$
  - `void ass(int n)` 把 `BitInt` 赋值为 `int`
  - `void astr(string s)` 把 `BigInt` 赋值为 `string`
- `BigInt ass(int n)` 将 `int` 转换为 `BigInt`
- `BigInt astr(string s)` 将 `string` 转换为 `BigInt`
- `BigInt oppo(BigInt a)` 返回 $$a$$ 的相反数 
- `BigInt abs(BigInt a)` 返回 $$a$$ 的绝对值 
- `BigInt half(BigInt a)` 返回 $$a$$ 的二分之一
- `BigInt Plus(BigInt a,BigInt b)` 返回 $$a+b$$
- `BigInt Sub(BigInt a,BigInt b)` 返回 $$a-b$$
- `BigInt Mul(BigInt a,BigInt b)` 返回 $$a\times b$$
- `BigInt Div(BigInt a,BigInt b)` 返回 $$\lfloor\frac{a}{b}\rfloor$$
- `BigInt Power(BigInt a,BigInt b)` 返回 $$a^b$$
- `BigInt Sqrt(BigInt a,BigInt b)` 返回 $$\sqrt[b]{a}$$ （暂时复杂度较高，到时候改进）
- `bool csi(BigInt a,BigInt b)` 比较 $$a,b$$ 大小，$$a$$ 大返回 `true` 
- `bool equ(BigInt a,BigInt b)` 返回 `a==b` 
- `bool cod(BigInt a)` 返回 $$a$$ 的奇偶性，奇数返回 `true`

## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=20005;
struct BigInt{
	int len; // 长度 
	bool f; // 负数标记 
	int a[N]; // 高精度数组 
	void clear(){ // 清空 
		len=0;
		f=0;
		memset(a,0,sizeof(a));
		return;
	}
	void scan(){ // 读入 
		int d[N];
		clear();
		char c=getchar();
		while((c<'0'||c>'9')&&c!='-'){
			c=getchar();
		}
		if(c=='-'){
			f=1;
			c=getchar();
		}
		while(c>='0'&&c<='9'){
			d[++len]=c-'0';
			c=getchar();
		}
		for(int i=len;i>=1;i--){
			a[len-i+1]=d[i];
		}
		chzero();
		return;
	}
	void print(char c){ // 输出，并以参数 c 结尾，如果 c 为 ? 则不输出任何字符
		if(f){
			putchar('-');
		}
		for(int i=len;i>=1;i--){
			putchar(a[i]+'0');
		}
		if(c!='?')putchar(c);
		return;
	}
	void dzero(){ // 删除前导零 
		while(!a[len]&&len>1)len--;
		return;
	}
	void chzero(){ // 将 -0 转换为 0 
		if(len==1){
			if(!a[len]){
				f=0;
			}
		}
	}
	void ass(int n){ // 将 BigInt 赋值为 int 
		clear();
		if(n<0){
			f=1;
			n=-n;
		}
		while(n){
			a[++len]=n%10;
			n/=10;
		}
		if(!len){
			len++;
		}
		return;
	}
	void astr(string s){ // 将 BigInt 赋值为 string 
		clear();
		if(s[0]=='-'){
			f=1;
			s.erase(0,1);
		}
		len=s.size();
		for(int si=s.size(),i=si-1;i>=0;i--){
			a[si-i]=s[i]-'0';
		}
		chzero();
		dzero();
		return;
	}
};

BigInt ass(int n); // 将 int 转换为 BigInt 
BigInt astr(string s); // 将 string 转换为 BigInt 
BigInt oppo(BigInt a); // 返回 a 的相反数 
BigInt abs(BigInt a); // 返回 a 的绝对值 
BigInt half(BigInt a); // 返回 a 的二分之一 
BigInt Plus(BigInt a,BigInt b); // 返回 a+b
BigInt Sub(BigInt a,BigInt b); // 返回 a-b
BigInt Mul(BigInt a,BigInt b); // 返回 a*b 
BigInt Div(BigInt a,BigInt b); // 返回 a/b 
BigInt Power(BigInt a,BigInt b); // 返回 a 的 b 次方 
BigInt Sqrt(BigInt a,BigInt b); // 返回 a 的 b 次方根 
bool csi(BigInt a,BigInt b); // 比较 a b 大小，a 大返回 true
bool equ(BigInt a,BigInt b); // 返回 a==b 
bool cod(BigInt a); // 返回 a 的奇偶性，奇数返回 true 

BigInt ass(int n){
	BigInt ans;
	ans.ass(n);
	return ans;
}
BigInt astr(string s){
	BigInt ans;
	ans.astr(s);
	return ans;
}
BigInt oppo(BigInt a){
	a.f=!a.f;
	a.chzero();
	return a;
}
BigInt abs(BigInt a){
	a.f=0;
	return a;
}
BigInt half(BigInt a){
	for(int i=a.len;i>=1;i--){
		a.a[i-1]+=a.a[i]%2*10;
		a.a[i]/=2;
	}
	a.a[0]=0;
	a.dzero();
	return a;
} 
bool csi(BigInt a,BigInt b){
	if(a.f^b.f){
		return b.f;
	}
	if(a.len>b.len){
		return !a.f;
	}
	if(a.len<b.len){
		return a.f;
	}
	for(int i=a.len;i>=1;i--){
		if(a.a[i]>b.a[i]){
			return !a.f;
		}
		if(a.a[i]<b.a[i]){
			return a.f;
		}
	}
	return 0;
}
bool equ(BigInt a,BigInt b){
	if(a.f!=b.f)return 0;
	if(a.len!=b.len)return 0;
	for(int i=1;i<=a.len;i++){
		if(a.a[i]!=b.a[i])return 0;
	}
	return 1;
}
bool cod(BigInt a){
	return a.a[1]&1;
}
BigInt Plus(BigInt a,BigInt b){
	if(b.f^a.f){
		if(b.f){
			return Sub(a,oppo(b));
		}else{
			return Sub(b,oppo(a));
		}
	}
	BigInt ans;
	ans.clear();
	if(b.f&&a.f){
		ans.f=1;
		a=oppo(a);
		b=oppo(b);
	}
	ans.len=max(a.len,b.len);
	for(int i=1;i<=ans.len;i++){
		ans.a[i]+=a.a[i]+b.a[i];
		ans.a[i+1]+=ans.a[i]/10;
		ans.a[i]%=10;
	}
	if(ans.a[ans.len+1]>0){
		ans.len++;
	}
	return ans;
}
BigInt Sub(BigInt a,BigInt b){
	if(b.f^a.f){
		return Plus(a,oppo(b));
	}
	if(!a.f){
		if(csi(b,a)){
			return oppo(Sub(b,a));
		}
	}else{
		return oppo(Sub(oppo(a),oppo(b)));
	}
	BigInt ans;
	ans.clear();
	ans.len=max(a.len,b.len);
	for(int i=1;i<=ans.len;i++){
		ans.a[i]+=a.a[i]-b.a[i];
		while(ans.a[i]<0){
			ans.a[i+1]--;
			ans.a[i]+=10;
		}
	}
	ans.dzero();
	return ans;
}
BigInt Mul(BigInt a,BigInt b){
	BigInt ans;
	ans.clear();
	ans.len=a.len+b.len-1;
	ans.f=a.f^b.f;
	for(int i=1;i<=a.len;i++){
		for(int j=1;j<=b.len;j++){
			ans.a[i+j-1]+=a.a[i]*b.a[j];
		}
	}
	for(int i=1;i<=ans.len;i++){
		ans.a[i+1]+=ans.a[i]/10;
		ans.a[i]%=10;
		if(i==ans.len&&ans.a[ans.len+1]){
            ans.len++;
        }
	}
	ans.dzero();
	return ans;
}
BigInt Div(BigInt a,BigInt b){
	BigInt sum,ans;
	sum.clear();
	ans.clear();
	bool af=a.f^b.f;
	a=abs(a);
	b=abs(b);
	for(int i=a.len;i>=1;i--){
		sum=Plus(Mul(sum,ass(10)),ass(a.a[i]));
		ans=Mul(ans,ass(10));
		while(!csi(b,sum)){
			sum=Sub(sum,b);
			ans=Plus(ans,ass(1));
		}
	}
	ans.f=af;
	return ans;
}
BigInt Power(BigInt a,BigInt b){
	if(equ(b,ass(0)))return ass(1);
	if(equ(b,ass(1)))return a;
	BigInt d=Power(a,half(b));
	d=Mul(d,d);
	if(cod(b))d=Mul(d,a);
	return d;
}
BigInt Sqrt(BigInt a,BigInt b){ // 懒得起名了，就叫 Sqrt 
	BigInt l,r;
	if(cod(b)){
		if(csi(ass(0),a)){
			r.ass(0);
			l=a;
		}else{
			r=a;
			l.ass(0);
		}
	}else{
		l.ass(0);
		r=a;
	}
	while(csi(r,Plus(l,ass(1)))){
		BigInt mid=Div(Plus(l,r),ass(2));
		if(csi(Power(mid,b),a)){
			r=mid;
		}else{
			l=mid;
		}
	}
	if(csi(Power(r,b),a))return l;
	else return r;
} 
int main(){
	
	return 0;
}
```

