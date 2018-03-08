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
