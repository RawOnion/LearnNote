1. `tensor`张量

多维数组



2. `flow`流

张量之间通过计算而转换的过程



3. `tensorflow`通过**计算图**来构造模型

计算图中的每一个节点都是计算集合

节点之间的边描述了计算节点之间的关系



4. 计算图是一个有向图，由以下内容构成：

- 一组节点，每个**节点**都代表一个**操作**，是一个**运算**
- 一组有向边，每条边描述了**节点**之间的关系(**数据传递和控制依赖**)



5. `tensorflow`有两种边：

- **常规边**：代表数据依赖关系。一个节点的运算输出成为另一个节点的输入，两个节点之间有`tensor`流动(**值传递**)
- **特殊边**：不携带值的传递，表示两个节点之间的控制相关性。



例子：

```python
import tensorflow as tf
node1=tf.constant(3.0,tf.float32,name="node1")
node2=tf.constant(4.0,tf.float32,name="node2")
node3=tf.add(node1,node2)

#创建计算图就是建立计算模型,执行会话才能提供数据并获得结果
#建立对话并显示运行结果
sess=tf.Session()
print("运行sess.run(node1)的结果：",sess.run(node1))

#更新变量并返回计算结果
print("运行sess.run(node3)的结果：",sess.run(node3))

#关闭session
sess.close()
```

