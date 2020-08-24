在`numpy.array()`中，`+、*`表示对`array`中的每个元素进行加和乘元素。

在Python的`list`中，`+、*`表示对两个`list`进行连接和对`list`中的元素进行重复。

```python
import numpy as np
a=[1,2,3]

b=np.array([1,2,3])
print(a+[4])
print(b+1)

print(a*2)
print(b*2)
'''
[1, 2, 3, 4]
[2 3 4]
[1, 2, 3, 1, 2, 3]
[2 4 6]
'''
```



在`numpy.array()`中，取`array`中的元素`b[0,1]`和`b[0][1]`均可以。

在Python的`list`中，取`list`中的元素只能使用`a[0][1]`。

```python
import numpy as np
a=[[2,3],[4,5],[6,7]]

b=np.array([[2,3],[4,5],[6,7]])

print(a[0][1])

print(b[0,1])
print(b[0][1])
'''
3
3
3
'''
```

