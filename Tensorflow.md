# Tensorflow 相关笔记

## 基础知识
* 基本属性  

  * Graph

    使用**图(graph)** 来表示计算任务.有边与点;圆圈代表常亮(const);椭圆代表操作( Op) ;圆角方框代表子图;边代表张量的流向,边上的标记代表张量的形状,(其中,若张量1阶,标记为 scalar, 高阶的标记为 m*n)

  * 在被称之为**会话(Session)** 的**上下文(context)** 中执行图.<br>

    Session: 用于执行图.每次 sess.run 的时候才进行真正的计算

  * 使用 **tensor** 表示数据.

    零阶张量为scalar 如[1], 一阶张量 vector如[1,2,3,],二阶张量 matrix,

  * Variable

    通过 **变量 (Variable)** 维护状态.

    表达,更新,存储模型参数.其可变更, 初始化时被添加默认的 collection 中.

    在整个 session 运行前, Graph 中所有 variable 必须被初始化

    ```shell
    sess = tf.Session()
    init = tf.initialize_all_variables() 
    sess.run(init)
    ```

    tensorflow 中定义某个字符串为变量后它才是变量,与 python 不同.

  * Tensor: 类型化的多维数组,图的边. <br>

  * Operation

    执行计算的单元,节点. 在 run 之后才会执行.

  * 使用 feed 和 fetch 可以为任意的操作(arbitrary operation) 赋值或者从其中获取数据.

    feed一般使用字典形式临时替换值,在该方法结束后自动失效.<br>

  * collection

    用来组织不同类别的对象,提供一种零存整取思路,在每个层次可以创造对象,存入相应 collection 中;创造完成后可以统一从一个 collection 中取出一类变量,进而施加操作.

    在 tf.GraphKeys 中包含了所有默认 collections 的名称. Variable 被手机在名为 tf.GraphKeys.VARIABLES中.

  * placeholder

    是占位符号,暂时存储变量.从外部传入 data, 使用字典传入.

* 数据结构    
  Rank指数据的维度;shape 指tensor 每个维度的数据个数; Data type 指单个数据的类型,浮点整形等; <br>
  * Variables <br>
    在训练模型时保存于更新参数.<br>
  * placeholders 与 feed_dict <br>
    定义一张 graph 时候,有时候不需要计算的值,比如输入数据,开始并没有值.所以需要这两个函数的帮助.
    tf.placeholder(dtype,shape=None,name=None)

* 初始化常见操作例子

  ```shell
  #定义变量
  state = tf.Variable(0, name='counter')
  Weights = tf.Variable(tf.random_uniform([1], -1.0, 1.0))
  biases = tf.Variable(tf.zeros([1]))
  #定义常量
  matrix1 = tf.constant([[3,3]])
  matrix2 = tf.constant([[2],
                         [2]])
  ```

  ​

## 常见函数记录
* tf.assign(x,y):把 x 的值变为 y 的值.
* tf.reduce_mean(input_tensor, reduction_indices=None, keep_dims=False, name=None)      
在输入张量的某个维度上进行求平均值,得出结果为一个标量数据. 第二个为某个维度

## 关于 Tensorboard
* 基本操作
  *  tf.summary

      summary 是对网络中 tensor 取值进行监测的一种 Operation, 不影响数据流本身.

      * tf.summary.scalar 记录标量: tf.summary.scalar(tags, values, collections=None, name=None) 
      * tf.summary.histogram 记录数据直方图: tf.summary.histogram(tag, values, collections=None, name=None)
      * tf.summary.distribution 记录数据的分布图<br>
      * tf.summary.image 记录图像数据: tf.summary.image(tag, tensor, max_images=3, collections=None, name=None)

  * tf.summary.merge(inputs, collections=None, name=None)        

      tf.summary.merge_all 将所有 summary 节点合并成一个节点,只要运行这个节点,就能产生之前所有的 summary data. 不需要单独run 每个 Op.

  * 使用 tf.summary.FileWriter 将运行后输出的数据保存到本地.  

* 概念

  * histogram:

   统计 Tensor 的取值分布. Distribution 显示取值范围; histogram 中显示细节的取值概率信息.二者是对同一数据的不同方式展现.

  * name_scope()

    保证数据流图简洁,将一些子图归类为一个子节点.

 * 输出参数图表基本代码
 ```python
 #  step1  本段代码展示输出图表的基本方法
 with tf.name_scope('layer_name')
   with tf.name_scope('weights')
     Weights=...
     tf.summary.histogram('name',Weights) # 把 Weights 加到 histogram 中
 
 with tf.name_scope('loss')
   loss=...
   tf.summary.scalar('loss',loss) # 把 loss 加到 scalar 中展示
   
 #  step2  融合节点,写入 log
 merged=tf.summary.merge_all()
 writer=tf.summary.FileWriter('logs/',sess.graph)
 
 #  step3  在训练或学习过程中,每过一定步数,记录一下数据 
 result=tf.sess.run(merged,feed_dict={,})  #字典中数据与训练的输入数据一样
 writer.add_summary(result,步数)
 
 ```

## Error记录

- 重复运行程序时出错  	

```shell
ValueError: Variable conv1/weights already exists, disallowed. Did you mean to set reuse=True in VarScope? Originally defined at:...
```

​	解决办法:在程序段前加  
	`tf.reset_default_graph()`