# Tensorflow 笔记

## 在重复运行程序时候,会出现如下错误
ValueError: Variable conv1/weights already exists, disallowed. Did you mean to set reuse=True in VarScope? Originally defined at:
解决办法:在程序前加
`tf.reset_default_graph()`
