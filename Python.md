# Python 中函数以及一些库的使用

[TOC]

## 常用函数 

* `assert`

  断言, 其后面的判断为假时候就出现错误.是编程序时候用的检查程序的作用.后面为真,则什么都不做.

* `hasattr()` 
  用于确定一个对象中是否具有某个属性,返回一个布尔值    `hasattr(object,name)`   

* `idxmax() ` 
  返回最大值的索引

* `flatten`

  处理矩阵或数组,把其降到一维,默认横着方向降维原数据,若按竖着方向处理源数据, `flatten('F')`

## 一些库

* `shutil` :高层次文件操作工具

## Numpy

- `np.newaxis` :增加一个维度.

- `np.random.permutation(state_action.imdex)  ` 
  洗牌功能,打乱次序. index 与 columns 对应, index 是 row 的标签  

- `np.random.choice(a, size=None, replace=True, p=None)`

  从 a 中随机算去size 个量,结果放入 array 中返回. p 是可以设置出现概率.

- `np.clip(a, a_min, a_max, out=None)`

  把a 中小于 a_min 的值用 a_min 代替,把大于 a_max 的值用a_max 代替.

## 零散知识
* python 中小括号代表元组;中括号代表列表;大括号代表字典.
* 引用同级文件夹下的 py 文档
```python
import sys 
sys.path.append("..")
from <文件夹>.<py文件> import <模块>
```
* 有关下划线
  + 单下划线    
  用在循环中计数中,但是对它的值并不关心,而且在下文不会调用此值时,习惯用\_
  + 名称前的下划线(如: \_shahriar)  
  指定该名称属性为私有,仅供内部使用.视为 API 中非公开部分,在修改他们时无需对外部通知.  
  + 名称前的双下划线(\_\_shahriar)  
  这种用法不是惯例,对解释器来说有特定含义,避免与子类定义的名称冲突.不太懂
  + 名称前后的双下划线(\_\_init\_\_)  
  这种用法表示 Python 中特殊的方法名.是一种惯例.这将确保不会与用户自定义的名称冲突.   

* python3 与 2 区别   
  python3中使用 print("")  
  python2中    print ""  

* python 中的 None   <br>
  它既不是0，也不是False，也不是空字符串。它只是一个空值的对象，也就是一个空的对象，只是没有赋值而已。 

* 哈希?

  哈希表是一种能实现关联数组的抽象数据结构，能把很多「键」映射到很多「值」上。哈希表使用哈希函数来计算索引，一个索引对应一个值。

* 类 class

  类是抽象模板,类名的括号里表示从哪个类继承下来的.\__init__方法第一个参数永远是 self;

  如果让内部属性不被外部访问,就可以把属性的名称前加两个下划线,就成为了私有变量.只有内部可以访问.

  前后都有两个下划线的变量名是特殊变量;以单个下划线开头的变量是外部可以访问的.他的实际含义是:虽然我可以被访问,但是请把我视为私有变量,不要随意访问.

  类中定义的功能称之为方法.

* 类中函数的互相调用小结

  在勒种的定义实例方法时要加一个 self 参数.

## 有关 matplotlib 画图
* 绘制多个独立窗口图表
为不同窗口图标起不同名字,为里添加内容.并在程序最终统一显示,即刻绘制多个独立窗口表格
```python
# figure1
plt.figure('figure1')
plt.plot(np.arange(len(self.qtarget_his)),self.qtarget_his,c='r',label='DQN Q eval')
plt.legend(loc='best') #设置图例,自动分配
plt.ylabel('Q_target value')
plt.xlabel('training steps')
# figure2
plt.figure('cost')
plt.plot(np.arange(len(self.cost_his)), self.cost_his)
plt.legend(loc='best')
plt.ylabel('Cost')
plt.xlabel('training steps')
# 程序最后显示窗口
plt.show()
```
* 保存图表   
```python
plt.plot()
plt.savefig('PATH and name.jpg')
plt.show
```
