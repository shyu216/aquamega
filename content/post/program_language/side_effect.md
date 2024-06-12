---
date: 2024-06-11
draft: false
title: Side Effect
tags: 
    - Program Language
params:
  math: true
---


在编程中，"副作用"（Side Effect）是指函数或表达式在计算结果以外，对外部世界产生的影响。这些影响可能包括更改全局变量的值，修改输入参数，执行 I/O 操作，等等。
在 Python 中，许多操作和函数都可能产生副作用。以下是一些常见的例子：

1. **修改全局变量**：在函数内部修改全局变量的值会产生副作用。

```python
x = 1

def change_global():
    global x
    x = 2

change_global()
print(x)  # 输出：2
```

2. **修改可变类型的参数**：如果函数接收一个可变类型（如列表或字典）的参数，并修改了它，那么这就是一个副作用。

```python
def add_element(my_list, element):
    my_list.append(element)

numbers = [1, 2, 3]
add_element(numbers, 4)
print(numbers)  # 输出：[1, 2, 3, 4]
```

3. **I/O 操作**：读写文件、打印到控制台、网络请求等 I/O 操作都会产生副作用。

```python
def write_to_file():
    with open('file.txt', 'w') as f:
        f.write('Hello, World!')

write_to_file()  # 这将在磁盘上创建或修改一个文件
```

4. **修改类的实例属性**：在类的方法中修改实例属性也是一种副作用。

```python
class MyClass:
    def __init__(self):
        self.value = 0

    def increment(self):
        self.value += 1

obj = MyClass()
obj.increment()
print(obj.value)  # 输出：1
```

在编程时，我们通常应尽量避免副作用，因为它们会使代码更难理解和测试。无副作用的函数（也称为纯函数）只依赖于输入参数，并且只通过返回值与外部世界交互，这使得它们的行为更加可预测和可重用。