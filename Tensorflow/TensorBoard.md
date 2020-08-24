- TensorBoard是TensoFlow的可视化工具
- 通过TensorFlow程序运行过程中输出的日志文件可视化TensorFlow程序的运行状态
- TensorBoard和TensorFlow程序跑在不同的进程中

```python
'''
TensorBoard例子
'''

import tensorflow as tf

#清除以前生成的节点，相当于重启默认图
tf.reset_default_graph()

#logdir改为自己机器上的合适路径
logdir="D:/log"

#定义一个简单的计算图，实现向量加法操作
input1=tf.constant([1.0,2.0,3.0],name="input1")
input2=tf.Variable(tf.random_uniform([3]),name="input2")
output=tf.add_n([input1,input2],name="add")

#生成一个写日志的writer，并将当前的TensorFlow计算图写进日志
writer=tf.summary.FileWriter(logdir,tf.get_default_graph())
writer.close()
```



# TensorBoard使用方法：

TensorBoard不需要额外安装，在TensorFlow安装时已自动完成。

在 <font color=red size=30> Anaconda Prompt</font>(conda专用的终端)中运行`tensorflow --logdir=/path`，并将日志的地址指向程序日志输出的地址。
![](https://cdn.jsdelivr.net/gh/RawOnion/imgcloud/img/tensorboard使用方法.png)
启动服务的端口默认为6006；使用--port参数可以改变启动服务的端口。



如果google chrome打不开终端提示的地址，可以将地址改为：

```txt
# 解决办法1：
localhost:6006
# 解决办法2：
0.0.0.0:6006
```



# 参考

[1] [win10环境下tensorboard无法通过google浏览器打开的解决办法](https://blog.csdn.net/kakangel/article/details/88123823)

[2] [Tensorboard的安装及使用](https://blog.csdn.net/u012679707/article/details/79898530)