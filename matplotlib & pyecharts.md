# matplotlib & pyecharts

### 二维线性图、折线图：plot

```python3
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 1000)    # 自变量，1000个点
y = np.sin(x) + 1
z = np.cos(x**2) + 1

plt.figure(figsize=(8, 6))
plt.plot(x, y, label='sinx + 1', color='red', linewidth=2)
plt.plot(x, z, 'b--', label='cosx + 1', color='green')
plt.xlabel('次数')
plt.ylabel('Volt')
plt.title('cos & sin')
plt.ylim(-0.1, 2.1)
plt.legend()
plt.rcParams['font.sans-serif'] = ['SimHei']    # 可以正常显示中文
plt.show()
```
###  饼型图：pie

```python3
  import matplotlib.pyplot as plt
  
  lab = 'A', 'B', 'C', 'D'
  siz = [15,30,45,10]
  col = ['yellow', 'green', 'lightskyblue', 'lightcoral']
  expl = (0, 0.1, 0, 0)    # 突出显示 第二块, 数字越大，越突出
  plt.pie(siz, explode=expl, labels=lab, colors=col,
          autopct='%1.1f%%', shadow=True, startangle=90)
  plt.axis('equal')   # 避免被压缩成椭圆
  plt.show()
```

###  柱状图：hist

+ hist(x,y)：x待绘制的一维数组，y为整数时，表示均匀分为y组，y为列表时，表示分组的边界点。
+ ```python3
  import matplotlib.pyplot as plt
  
  x = [-1,-1,-1,0,0,1,2,3,4]
  y = [-3,-1,1,3]
  plt.hist(x, y, rwidth=0.8)	# y1<=x<y2，此时是左闭右开，但是在pandas.cut中为左开右闭
  plt.show()
  ```

###  通过画出带有一个横坐标，两个纵坐标的图，兼具柱状图和线图，分析pyecharts 和 matplotlib 异同

+ 原始在Excel中的数据catering_dish_profit.xls：

  | 菜品ID | 菜品名 | 盈利 |
  | ------ | ------ | ---- |
  | 17148  | A1     | 9173 |
  | 17154  | A2     | 5729 |
  | 109    | A3     | 4811 |
  | 117    | A4     | 3594 |
  | 17151  | A5     | 3195 |
  | 14     | A6     | 3026 |
  | 2868   | A7     | 2378 |
  | 397    | A8     | 1970 |
  | 88     | A9     | 1877 |
  | 426    | A10    | 1782 |

+  matplotlib 处理过程
```python3
import pandas as pd
import matplotlib.pyplot as plt

dish_profit = 'catering_dish_profit.xls'
data = pd.read_excel(dish_profit, index_col = u'菜品名')
data = data[u'盈利'].copy()
data.sort_values(ascending = False)

plt.rcParams['font.sans-serif'] = ['SimHei']
plt.rcParams['axes.unicode_minus'] = False

plt.figure()
data.plot(kind='bar')
plt.ylabel(u'盈利（元）')
p = 1.0*data.cumsum()/data.sum()

p.plot(color = 'r', secondary_y = True, style = '-o',linewidth = 2)
plt.annotate(format(p[6], '.4%'), xy = (6, p[6]), xytext=(6*0.9, p[6]*0.9), arrowprops=dict(arrowstyle="->", connectionstyle="arc3,rad=.2"))
plt.ylabel(u'盈利（比例）')
plt.show()
```
+   pyecharts 处理过程
```python3
import pandas as pd
from pyecharts import Bar, Line, Overlap

dish_profit = 'catering_dish_profit.xls'
data = pd.read_excel(dish_profit)
attr = data[u'菜品名']
v1 = data[u'盈利']
bar = Bar("")
bar.add("盈利(元)",attr,v1,is_stack=True,xaxis_rotate=30,yaxix_min=4.2,
    xaxis_interval=0,is_splitline_show=False)
data['rate'] = data[u'盈利'].cumsum()/data[u'盈利'].sum()
v2 = data['rate']

line = Line("盈利比例")
line.add("盈利比例",attr,v2,is_stack=True,xaxis_rotate=30,yaxix_min=4.2,
    mark_point=['min','max'],xaxis_interval=0,line_color='lightblue',
    line_width=4,mark_point_textcolor='black',mark_point_color='lightblue',
    is_splitline_show=False)
overlap = Overlap()
overlap.add(bar)
overlap.add(line,yaxis_index=1,is_add_yaxis=True)  # is_add_yaxis=True,右侧增加一排y坐标
overlap.render('菜品盈利.html')
```

+ 总结：pyecharts 画出的图显示在HTML中，比matplotlib画出的图更好看。
###  画柱状图的三种方式
+ pandas：       data.plot(kind='bar')
+ matplotlib：	hist(x,y)
+ pyecharts：	bar = Bar("")

###  箱型图绘制的两种方式

+ 直接调用DataFrame的boxplot： data.boxplot() 
+ 调用Series或DataFrame的plot，用kind指定为box：D.plot(kind = 'box')，D为DataFrame格式

### 误差条形图

+ D.plot(yerr=err)/D.plot(xerr=err)

+ ```python3
  import matplotlib.pyplot as plt
  import numpy as np
  import pandas as pd
  
  err = np.random.randn(10)
  y = pd.Series(np.sin(np.arange(10)))
  y.plot(yerr=err)	# 显示的是y方向的误差
  plt.grid()
  plt.show()
  ```

