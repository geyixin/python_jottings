# matplotlib & pyecharts

## 1. matplotlib 

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

## 2. 为了画出一个横坐标，两个纵坐标的图，兼具柱状图和线图，具体分析 pyecharts 和 matplotlib 异同

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

+ 2.1  matplotlib 处理过程
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
+ 2.2  pyecharts 处理过程
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