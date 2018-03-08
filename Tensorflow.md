# Tensorflow 笔记

## 问题
* 重复运行程序时出错
`ValueError: Variable conv1/weights already exists, disallowed. Did you mean to set reuse=True in VarScope? Originally defined at:...`  
解决办法:在程序前加
`tf.reset_default_graph()`
