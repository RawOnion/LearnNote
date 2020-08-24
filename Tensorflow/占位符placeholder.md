- TensorFlow中的**Variable变量类型**，在定义时需要初始化，但有些变量**定义时并不知道其数值**，只有当真正开始运行程序时，才由外部输入，比如训练数据，这时候需要用到**占位符**
- tf.placeholder**占位符**，是TensorFlow中特有的一种数据结构，类似动态变量，函数的参数、或者C语言或者Python语言中格式化输入出时的"%"占位符
- **占位符的作用：** 在训练过程中逐步把样本代入到优化器中。

`tf.placeholder(dtpye,shape=None,name=None)`

```python
import tensorflow as tf
x=tf.placeholder(tf.float32,[2,3],name="tx")
#生成一个2×3的二维数组，矩阵中每个元素的类型都是tf.float32，内部对应的符号名称是tx
```



# `feed`送入模型数据和从模型中取出数据

```python
import tensorflow as tf
a=tf.placeholder(tf.float32,name="a")
b=tf.placeholder(tf.float32,name="b")
c=tf.multiply(a,b,name="c")

with tf.Session() as sess:
    #通过feed_dict的参数传值,按字典格式
    result=sess.run(c,feed_dict={a:8.0,b:3.5})
    print(result)
```

```python
"多个操作可以通过一次Feed完成执行"
import tensorflow as tf

a=tf.placeholder(tf.float32,name="a")
b=tf.placeholder(tf.float32,name="b")
c=tf.multiply(a,b,name="c")
d=tf.subtract(a,b,name="d")

with tf.Session() as sess:
    
    result=sess.run([c,d],feed_dict={a:[8.0,2.0,3.5],b:[1.5,2.0,4.]})
print(result)
    #取结果中的第一个
print(result[0])

'''
[array([12.,  4., 14.], dtype=float32), array([ 6.5,  0. , -0.5], dtype=float32)]
[12.  4. 14.]
'''
```

```python
"一次返回多个值得第二种写法"
import tensorflow as tf

a=tf.placeholder(tf.float32,name="a")
b=tf.placeholder(tf.float32,name="b")
c=tf.multiply(a,b,name="c")
d=tf.subtract(a,b,name="d")

with tf.Session() as sess:
	#对结果直接解包
    rc,rb=sess.run([c,d],feed_dict={a:[8.0,2.0,3.5],b:[1.5,2.0,4.]})
print("value of rb=",rb,"value of rc=",rc)
```

