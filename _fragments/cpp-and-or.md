---
layout: fragment
title: 关于 C++ 的与和非
tags: [C++]
description: C++ 与和非
keywords: C++, and, or, 与和非
mathjax: true
---

C++ 在运行程序时，遇到 `0 && xxx` 或者 `1 || xxx` 时，会自动跳过后面的 `xxx`，而直接返回 `0` 或 `1` (这应该是大多数人都知道的吧)

我们可以写一段代码：

```cpp
#include<bits/stdc++.h>
using namespace std;
bool fun(){
    printf("Hello! World!\n");
    return 1;
}
int main(){
    printf("1:\n");
    cout<<(0&&fun())<<endl<<endl;
    printf("2:\n");
    cout<<(1&&fun())<<endl<<endl;
    printf("3:\n");
    cout<<(0||fun())<<endl<<endl;
    printf("4:\n");
    cout<<(1||fun())<<endl<<endl;
    return 0;
}
```

运行之后，输出结果是：

```
1:
0

2:
Hello! World!
1

3:
Hello! World!
1

4:
1
```

这证明了上面的规律
