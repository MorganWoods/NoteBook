# Python 中的函数
## hasattr()
用于确定一个对象中是否具有某个属性,返回一个布尔值  
`hasattr(object,name)`

# 有关 matplotlib 画图
## 绘制多个独立窗口图表
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
