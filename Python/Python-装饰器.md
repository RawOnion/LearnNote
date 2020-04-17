# Python-装饰器

## 装饰器定义

在代码运行期间动态增加功能的方式，称之为"装饰器"（Decorator）

概括的讲，装饰器的作用就是**为已经存在的函数对象添加额外的功能。**

**装饰器本质上是一个Python函数，它可以让其他函数在不需要做任何代码变动的前提下增加额外功能，装饰器的返回值也是一个函数对象（这点和闭包一样）**



我们要定义一个能打印日志的decorator，可以定义如下：

```python
def log(func):
    def wrapper(*args,**kw):
        print('call %s():'%func.__name__)
        return func(*args,**kw)
	return wrapper
```



观察上面的log，因为它是一个decorator，所以接受一个函数作为参数，并返回一个函数。我们要借助Python的@语法，把decorator置于函数的定义处：

```python
@log
def now():
    print('2015-3-25')
```



调用now()函数，不仅会运行now()函数本身，还会在运行now()函数前打印一行日志：

```python
>>>now()
call now():
2015-3-25
```



把`@log`放到`now()`函数的定义处，相当于执行了语句：

```python
now=log(now)
```



例如

```python
#python 3.6
#!/usr/bin/env python
# -*- coding:utf-8 -*-
def a(b):
    print("111111")
    b()
    print('222222')

#此处添加装饰器相当于执行了如下语句
#b=a(b)
#因为a()默认返回值为None,所以b的值为None
@a
def b():
    print("BBBBBB")
print(b)
#结果：
#111111
#BBBBBB
#222222
#None
```

```python
#python 3.6
#!/usr/bin/env python
# -*- coding:utf-8 -*-
def a(b):
    print("111111")
    b()
    print('222222')

def b():
    print("BBBBBB")

c = a(b)
print(c)
#结果
#111111
#BBBBBB
#222222
#None
```

由于`log()`是一个decorator，返回一个函数，所以，原来的`now()`函数仍然存在，只是现在同名的`now`变量指向了新的函数，于是调用`now()`将执行新函数，即在`log()`函数中返回的`wrapper()`函数。

## 需要传入参数的装饰器

如果decorator本身需要传入参数，那就需要编写一个返回decorator的高阶函数，写出来会更复杂。比如，要自定义log的文本：

```python
def log(text):
    def decorator(func):
        def wrapper(*args,**kw):
            print('%s %s():'%(text, func__name__))
            return func(*args,**kw)
        return wrapper
	return decorator
```



这个3层嵌套的decorator用法如下：

```python
@log('execute')
def now():
    print('2015-3-25')
```



执行结果如下：

```python
>>>now()
execute now()
2015-3-25
```



和两层嵌套的decorator相比，3层嵌套的效果是这样的:

```python
>>>now=log('execute')(now)
```



一个完整的decorator的写法如下：

```python
import functools
def log(func):
    #这句话的作用是wrapper.__name__=func.__name__
    #当使用now.__name__的时候显示的是now而不是wrapper
    @functools.wraps(func) 
    def wrapper(*args,**kw):
        print('call %s():'%func.__name__)
        return func(*args,**kw)
	return wrapper
```



或者针对带参数的decorator:

```python
import functools
def log(text):
	def wrapper(func):
        @functools.wraps(func)
        def wrapper1(*args,**kw):
            print('%s %s(): '%(text,func.__name__))
            return func(*args,**kw)
		return wrapper1

	return wrapper 
```



## Python中装饰器与Java中AOP的异同

装饰器与Java中的面向切面编程实现一样的功能。

AOP（Aspect-Oriented Programming，面向切面的编程），它是可以通过预编译或动态代理实现在**在不修改源代码的情况下给程序动态统一添加功能的技术。**

OOP（面向对象编程）是关注将需求功能划分为不同的并且相对独立、封装良好的类，并让它们有着属于自己的行为，依靠继承和多态等来定义彼此的关系；AOP是希望能够将通用需求功能从不相关的类当中分离出来，能够使得很多类共享一个行为，一旦发生变化，不必修改很多类，而只需修改这个行为即可。

AOP是使用切面（aspect）将横切关注点模块化，OOP是使用类将状态和行为模块化，在OOP的世界中，程序都是通过类和接口组织的。



## 参考

\[1\][廖雪峰Python装饰器](https://www.liaoxuefeng.com/wiki/1016959663602400/1017451662295584)

\[2\][详解Python的装饰器](https://www.cnblogs.com/cicaday/p/python-decorator.html)