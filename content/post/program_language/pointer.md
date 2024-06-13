---
date: 2024-06-11
draft: false
title: Pointer
tags: 
    - Program Language
---


在 C 语言中，指针是一个变量，其值为另一个变量的地址。以下是一个例子，演示了如何创建一个指向整数的指针 `dale`，并修改其指向的值 `xiaohuang` 和 `xiaodi`：

```c
#include <stdio.h>

int main() {
    int xiaohuang = 1;  // 定义一个整数变量 xiaohuang，并初始化为 1
    int xiaodi = 2;  // 定义一个整数变量 xiaodi，并初始化为 2
    int *dale = &xiaohuang;  // 定义一个指针变量 dale，并将其初始化为 xiaohuang 的地址

    printf("Before: xiaohuang = %d, xiaodi = %d\n", xiaohuang, xiaodi);  // 输出 xiaohuang 和 xiaodi 的初始值

    *dale = 0;  // 使用指针 dale 修改 xiaohuang 的值为 0

    dale = &xiaodi;  // 将 dale 的指向改为 xiaodi 的地址
    *dale = 0;  // 使用指针 dale 修改 xiaodi 的值为 0

    printf("After: xiaohuang = %d, xiaodi = %d\n", xiaohuang, xiaodi);  // 输出修改后的 xiaohuang 和 xiaodi 的值

    return 0;
}
```

在这个例子中，`&xiaohuang` 是取 `xiaohuang` 的地址，`*dale` 是取 `dale` 指向的值。所以 `*dale = 0;` 就是将 `dale` 指向的值（也就是 `xiaohuang`）改为 0。紧接着，`dale = &xiaodi;` 将 `dale` 的指向改为 `xiaodi` 的地址，然后 `*dale = 0;` 将 `dale` 指向的值（也就是 `xiaodi`）改为 0。