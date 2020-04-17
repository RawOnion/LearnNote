星号（asterisk）主要在函数定义和函数调用的时候使用：

1. 函数定义时

2. 1. 使用单个`*`会将所有的参数，放入一个元组（tuple）供函数使用。
   2. 使用两个 `**`会将所有的关键字参数，放入一个字典（dict）供函数使用。

3. 函数调用时

4. 1. 在list,tuple,set前加一个星号会把容器中的所有元素解包（unpack）变成位置参数。
   2. 在dict前加一个星号会把字典的键变成位置参数。
   3. 在dict前加两个星号会把字典的键值对变成关键字参数。



`a={'a':'Ass','b':'We','c':'Can'}`

###  `Aniki(*a)`

等同于`Aniki("a", "b", "c")`

### `Aniki(**a)`

等同于 `Aniki(a="Ass", b="We", c="Can")`

### `Aniki(**a,b=(1,2))`

等同于 `Aniki(a="Ass", b="We", c="Can",b=(1,2))`

```python
def keyword_only(*a):
    print(a)

a={'a':'Ass','b':'We','c':'Can'}
print(*a)
keyword_only(*a)
'''
a b c
('a', 'b', 'c')
'''
```



# 参考

[1] [Python函数中*和**的内涵究竟是什么呢?](https://www.zhihu.com/question/265519629)

