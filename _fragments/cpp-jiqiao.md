---
layout: fragment
title: C++ 小技巧
tags: [C++]
description: C++ 小技巧
keywords: C++, 技巧
mathjax: true
---

我们在写 C++ 代码时，经常会遇到一些需要使用 `long long` 的地方，有时候改起来比较麻烦，于是我推荐大家使用这种写法：

```cpp
#include<bits/stdc++.h>
#define int long long
using namespace std;
signed main(){
    
    return 0;
}
```

这里，我们用 `#define` 把 `int`  宏定义为 `long long`，

同时，我们要注意 `main` 函数的返回值必须是 `int`，所以把 `int main()` 改成 `signed main()`

那为什么可以这样改呢？

因为如果把 `int` 写全，其实就是 `signed int`，第一个词就是 `signed`，

所以 `int` = `signed int` = `signed`

---

再跟大家讲几个压行小技巧（不是认真的）

- `#include` 改为 `#import`。

- `return 0` 去掉。

- `using namespace std;` 去掉，并把一些代码前面加 `std::`（看情况使用）。

- `if(a){b;}else{c;}` 改成三目运算符，`a?b:c;`

- 多个 `if` 嵌套也可以用三目运算符：
  ```cpp
  if(a){
    if(b){
        c;
    }else{
        d;
    }
  }else{
    if(e){
        f;
    }else{
        g;
    }
  }
  ```

  可以改成： `a?(b?c:d):(e?f:g);`

**如果我的小技巧对大家有一点帮助，请大家在评论区回复 `作者好帅`**

感谢大家
