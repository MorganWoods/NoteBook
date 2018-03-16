# Tensorflow 相关笔记
 
## 知识
* 基础记录  
使用**图(graph)** 来表示计算任务.<br>
在被称之为**会话(Session)** 的**上下文(context)** 中执行图.<br>
使用 **tensor** 表示数据.<br>
通过 **变量 (Variable)** 维护状态.<br>
使用 feed 和 fetch 可以为任意的操作(arbitrary operation) 赋值或者从其中获取数据.<br>
feed一般使用字典形式临时替换值,在该方法结束后自动失效.<br>
## 常见函数记录<br>
* tf.assign(x,y):把 x 的值变为 y 的值.
## 问题
* 重复运行程序时出错  
```shell
ValueError: Variable conv1/weights already exists, disallowed. Did you mean to set reuse=True in VarScope? Originally defined at:...
```
解决办法:在程序段前加  
`tf.reset_default_graph()`

## 关于 Tensorboard
* 基本操作
	* 在 graph 中放置 summary operations 来记录信息 
	  使用 tf.summary.scalar 记录标量
	  使用 tf.summary.histogram 记录数据直方图
	  使用 tf.summary.distribution 记录数据的分布图
	  使用 tf.summary.image 记录图像数据
	* 使用 tf.summary.merge_all 将所有 summary 节点合并成一个节点,只要运行这个节点,就能产生之前所有的 summary data.
	* 使用 tf.summary.FileWriter 将运行后输出的数据保存到本地.  
 * 输出图表基本代码
 ```python
 #  step1  本段代码展示输出图表的基本方法
 with tf.name_scope('layer_name')
   with tf.name_scope('weights')
     Weights=...
     tf.summary.histogram('name',Weights)
 
 with tf.name_scope('loss')
   loss=...
   tf.summary.scalar('loss',loss)  
   
 #  step2  融合节点,写入 log
 merged=tf.summary.merge_all()
 writer=tf.summary.FileWriter('logs/',sess.graph)
 
 #  step3  在训练或学习过程中,每过一定步数,记录一下数据 
 result=tf.sess.run(merged,feed_dict={,})  #字典中数据与训练的输入数据一样
 writer.add_summary(result,步数)
 
 ```
