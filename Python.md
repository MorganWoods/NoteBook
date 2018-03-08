# Python 中函数以及一些库的使用
## 函数 
* hasattr()
用于确定一个对象中是否具有某个属性,返回一个布尔值  
`hasattr(object,name)`

## 功能记录
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
