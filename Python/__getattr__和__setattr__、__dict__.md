## `__dict__`属性

`__dict__`属性用于查看对象内部存储的所有属性名和属性值组成的字典。

```python
class Item:
    def __init__ (self, name, price):
        self.name = name
        self.price = price
im = Item('鼠标', 28.9)

#直接输出对象内部存储的所有属性名和属性值组成的字典
print(im.__dict__)  
# 通过__dict__访问name属性
print(im.__dict__['name'])
# 通过__dict__访问price属性
print(im.__dict__['price'])
im.__dict__['name'] = '键盘'
im.__dict__['price'] = 32.8
print(im.name) # 键盘
print(im.price) # 32.8
'''
{'name': '鼠标', 'price': 28.9}
鼠标
28.9
键盘
32.8
'''
```



## `__getattr__`、`__setattr__`

当程序操作(包括访问、设置、删除)对象属性时，Python系统同样会执行该对象特定的方法。

- `__getattribute__(self,name)`:当程序访问对象的`name`属性时被自动调用。
- `__getattr__(self,name)`:当程序访问对象`name`属性且该属性不存在时被自动调用。
- `__setattr__(self,name)`:当程序对对象的`name`属性赋值时被自动调用。
- `__delattr__(self,name)`:当程序删除对象的`name`属性时被自动调用



对于`__getattr__()`方法：**它只处理访问指定属性且该属性不存在的情形。**比如程序访问`width`或`height`属性，`Rectangle`对象本身包含该属性，因此该方法不会被触发。所以重写该方法只需处理我们需要“合成”的属性(比如`size`)，假如程序试图访问其他不存在的属性，直接引发`AttributeError`异常即可。

对于`__setattr__()`方法，**只要程序试图对指定属性赋值时总会触发该方法，因此无论程序是对`width`、`height`属性赋值，还是对`size`属性赋值，该方法都会被触发**。所以重写该方法既要处理对`size`属性赋值的情形，也要处理对`width`、`height`属性赋值的情形。**尤其是处理对`width`、`height`属性赋值的时候，千万不要在`__setattr__()`方法中再次对`width`、`height`赋值，因为对这两个属性赋值会再次触发`__setattr__()`方法，这样会让程序陷入死循环中。**

```python
class Rectangle:
    def __init__ (self, width, height):
        #这里的赋值会调用self.__setattr__("width",width)方法
        #self.__setattr__("height",height)
        self.width = width
        self.height = height
    def __setattr__(self, name, value):
        print('----设置%s属性----' % name)
        if name == 'size':
            self.width, self.height = value
        else:
            #这里不能用self.width=width
            #否则会陷入死循环
            self.__dict__[name] = value
    def __getattr__(self, name):
        print('----读取%s属性----' % name)
        if name == 'size':
            return self.width, self.height
        else:
            raise AttributeError
    def __delattr__(self, name):
        print('----删除%s属性----' % name)
        if name == 'size':
            self.__dict__['width'] = 0
            self.__dict__['height'] = 0
    
#这里在调用构造方法赋值是会调用__setattr__()方法
rect = Rectangle(3, 4)

#调用rect.__getattr__("size")
print(rect.size)

#调用rect.__setattr__("size",(6,8))方法
rect.size = 6, 8

#不会调用__getattr__()方法
print(rect.width)

#调用rect.__delattr__("size")方法
del rect.size

#调用rect.__getattr__("size")方法
print(rect.size)

'''
----设置width属性----
----设置height属性----
----读取size属性----
(3, 4)
----设置size属性----
----设置width属性----
----设置height属性----
6
----删除size属性----
----读取size属性----
(0, 0)
'''
```



如果程序需要在读取、设置属性之前进行某种拦截处理(比如检查数据是否合法之类的)，也可通过重写`__setattr__()`或`__getattr__()`方法来实现。

```python
class User:
    def __init__ (self, name, age):
        self.name = name
        self.age = age
    # 重写__setattr__()方法对设置的属性值进行检查
    def __setattr__ (self, name, value):
        # 如果正在设置name属性
        if name == 'name':
            if 2 < len(value) <= 8:
                self.__dict__['name'] = value
            else:
                raise ValueError('name的长度必须在2～8之间')
            
        elif name == 'age':
            if 10 < value < 60:
                self.__dict__['age'] = value
            else:
                raise ValueError('age值必须在10～60之间')
            
u = User('fkit', 24)
print(u.name)
print(u.age)
#u.name = 'fk' # 引发异常
#u.age = 2  # 引发异常

'''
fkit
24
'''
```

