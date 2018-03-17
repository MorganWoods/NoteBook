# Tensorflow 相关笔记
 
## 知识
* 基础记录  
使用**图(graph)** 来表示计算任务.<br>
在被称之为**会话(Session)** 的**上下文(context)** 中执行图.<br>
使用 **tensor** 表示数据.<br>
通过 **变量 (Variable)** 维护状态.<br>
Tensor: 类型化的多维数组,图的边. <br>
Operation: 执行计算的但愿,节点.<br>
Graph: 有边与点的图.<br>
Session: 用于执行图.每次 sess.run 的时候才进行真正的计算.<br>
使用 feed 和 fetch 可以为任意的操作(arbitrary operation) 赋值或者从其中获取数据.<br>
feed一般使用字典形式临时替换值,在该方法结束后自动失效.<br>
* 数据结构   <br>
Rank指数据的维度;shape 指tensor 每个维度的数据个数; Data type 指单个数据的类型,浮点整形等; <br>
	* Variables <br>
	  在训练模型时保存于更新参数.<br>  
  	* placeholders 与 feed_dict <br>
	  定义一张 graph 时候,有时候不需要计算的值,比如输入数据,开始并没有值.所以需要这两个函数的帮助.<br>
	  tf.placeholder(dtype,shape=None,name=None)<br>
  
  
## 常见函数记录<br>
* tf.assign(x,y):把 x 的值变为 y 的值.
* tf.reduce_mean(input_tensor, reduction_indices=None, keep_dims=False, name=None)      <br> 
在输入张量的某个维度上进行求平均值,得出结果为一个标量数据. 第二个为某个维度

## 问题
* 重复运行程序时出错  
```shell
ValueError: Variable conv1/weights already exists, disallowed. Did you mean to set reuse=True in VarScope? Originally defined at:...
```
解决办法:在程序段前加  
`tf.reset_default_graph()`

## 关于 Tensorboard
* 基本操作
	* 在 graph 中放置 summary operations 来记录信息 <br>
	  使用 tf.summary.scalar 记录标量: tf.summary.scalar(tags, values, collections=None, name=None) <br>
	  使用 tf.summary.histogram 记录数据直方图: tf.summary.histogram(tag, values, collections=None, name=None）<br>
	  使用 tf.summary.distribution 记录数据的分布图<br>
	  使用 tf.summary.image 记录图像数据: tf.summary.image(tag, tensor, max_images=3, collections=None, name=None)<br>
	* 使用 tf.summary.merge_all 将所有 summary 节点合并成一个节点,只要运行这个节点,就能产生之前所有的 summary data. <br>				tf.summary.merge(inputs, collections=None, name=None)<br>
	* 使用 tf.summary.FileWriter 将运行后输出的数据保存到本地.  <br>

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

