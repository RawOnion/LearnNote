**常量**
在运行过程中值不会改变的单元,在TensorFlow中无需进行初始化操作。
创建语句：
`constant_name=tf.constant(value)`



**变量**
在运行过程中值会改变的单元，在TensorFlow中需进行初始化操作。
创建语句：
`name_variable=tf.Variable(value,name)`



单个变量初始化:
`init_op=name_variable.initalizer()`
所有变量初始化：
`init_op=tf.global_variables_initializer()`

```python
import tensorflow as tf

node1=tf.Variable(3.0,tf.float32,name="node1")
node2=tf.Variable(4.0,tf.float32,name="node2")
result=tf.add(node1,node2,name="add")

sess=tf.Session()

#变量初始化
#init也是一个节点，在没有放入会话进行运行之前，都是静态图
init=tf.global_variable_initializer()
sess.run(init)
#只有运行run之后才会初始化完毕

print(sess.run(result))
```



