# pandas

+ pandas基本数据结构：Series，DataFrame
+ Series，就是列，类似一维数组，每个Series都有唯一表头，用来表示不同的Series
+ DataFrame，类似二维表格，每一列都是是个Series
+ Index，是为了定位Series中的元素，类似SQL中的主键，可以是字母、中文等，不一定数字


##  Series、DataFrame、index、colums、head、tail、describe、read_excel、index_col等

```python3
import pandas
s = pandas.Series([1,2,3], index=['a','b','c'])	# index 是每行的标号，不写默认从0开始标
print(s)	# 构建一个Series，直观显示就是一列，但是有标号
'''
a    1
b    2
c    3
dtype: int64
'''
print('--------------')
d = pandas.DataFrame([[1,2,3],[4,5,6]],columns=['a','b','c']) 
# colums是列的标号，不写默认从0开始标
d2 = pandas.DataFrame(s)
print(d.head())		# 默认输出前五行，也可以自己加数字 head(10),则可输出前十行
print(d.tail())
print('--------------')
'''
   a  b  c
0  1  2  3
1  4  5  6
'''
print(d.describe())		# 对d做简约分析，最大值，最小值，均值等等
p = pandas.read_excel('data.xlsx', index_col=u'菜品名称')
print(p.head(2))	# 打印表格的前两行
'''
菜品ID  菜品名  盈利
17148	A1	  9173
17154	A2	  5729
109  	A3	  4811
117 	A4	  3594
17151	A5	  3195
14	    A6	  3026
2868	A7	  2378
397 	A8	  1970
88  	A9	  1877
426	    A10	  1782
原数据中，”菜品名称“在第二列，那用 index_col=u'菜品名称'，则会把第二列变成第一列，
即实现以“菜品名称”索引，即“菜品名称”不再作为表格中的有效内容，仅作为索引
data = data[u'盈利'].copy()
新的data将会只含以“菜品名称”为index，以“盈利”为内容的两列数据：
print(data.head(15))	# 15只要超过data长度，则会把data全显示
则：
菜品名
A1     9173
A2     5729
A3     4811
A4     3594
A5     3195
A6     3026
A7     2378
A8     1970
A9     1877
A10    1782
Name: 盈利, dtype: int64
'''
```

##  cumsum，groupby

+ cumsum，依次给出前1、2、。。。、n个数的和

```python3
data['sum_Times'] = data['Times'].groupby(['userID']).cumsum()
原data:				
'''
    ID  Times
0   A   2
1   B   1
2   B   2
3   C   3
4   A   3
5   B   1
6   D   5
7   A   6
'''
现在data：
'''
    ID  Times   sum_Times
0   A   2       2
1   B   1       1
2   B   2       3
3   C   3       3
4   A   3       5
5   B   1       4
6   D   5       5
7   A   6       11
'''
```

##  相关系数中的 判定系数法
+ 三种常见的二元变量相关系数分析法：Pearson相关系数、Spearman秩相关系数、判定系数。
+ 正态分布假设下，Pearson和Spearman效率上等价；对于连续测量数据，Spearman更适用。
+ corr：计算数据样本的Spearman（Pearson）相关系数矩阵，data.corr(method='pearson')，支持pearson（皮尔森相关系数，默认选项），kendall（肯德尔系数），spearman（斯皮尔曼系数）。

| 日期      | 百合酱蒸凤爪 | 翡翠蒸香茜饺 | 金银蒜汁蒸排骨 | 乐膳真味鸡 | 蜜汁焗餐包 | 生炒菜心 | 铁板酸菜豆腐 | 香煎韭菜饺 | 香煎罗卜糕 | 原汁原味菜心 |
| --------- | ------------ | ------------ | -------------- | ---------- | ---------- | -------- | ------------ | ---------- | ---------- | ------------ |
| 2015/1/1  | 17           | 6            | 8              | 24         | 13         | 13       | 18           | 10         | 10         | 27           |
| 2015/1/2  | 11           | 15           | 14             | 13         | 9          | 10       | 19           | 13         | 14         | 13           |
| 2015/1/3  | 10           | 8            | 12             | 13         | 8          | 3        | 7            | 11         | 10         | 9            |
| 2015/1/4  | 9            | 6            | 6              | 3          | 10         | 9        | 9            | 13         | 14         | 13           |
| 2015/1/5  | 4            | 10           | 13             | 8          | 12         | 10       | 17           | 11         | 13         | 14           |

```python
data = 'data.xls'
data = pd.read_excel(data, index_col = u'日期')

p = data.corr() # 相关系数矩阵，即给出了任意两款菜式之间的相关系数
q = data.corr()[u'百合酱蒸凤爪'] # 只显示“百合酱蒸凤爪”与其他菜式的相关系数
r = data[u'百合酱蒸凤爪'].corr(data[u'翡翠蒸香茜饺']) # 计算“百合酱蒸凤爪”与“翡翠蒸香茜饺”的相关系数
print(p,'\n','-----------','\n',q,'\n','-----------','\n',r)
```

## 根据某一列的某个字段删除该行

>|  ID   |   A    |     B     |  C   |   D   |
>| :---: | :----: | :-------: | :--: | :---: |
>| 54993 | 234188 |  580717   | 432  | 5234  |
>| 28065 |   0    |     0     | 432  |  54   |
>| 55106 | 164982 |  283712   |  0   |   0   |
>| 21189 | 125500 |  281336   |  0   | 68578 |
>| 39546 |   0    |   5646    | 685  |  475  |
>| 56972 | 76946  |  294585   | 2423 |  432  |
>| 44924 | 287042 |     0     | 234  |   0   |
>| 22631 | 287230 | 276335.43 |  43  |  32   |
>| 32197 | 87401  |  321489   |  41  |  234  |
>
>+ 看print输出，感受如何执行的。
>
>```python3
>import pandas as pd
>
>data = pd.read_csv('../data/air_data_small.csv', encoding='utf-8')
>
>data = data[data['A'].notnull()*data['B'].notnull()]	# 保留非空
>index1 = data['A'] != 0     # 找到A列不为0
>index2 = data['B'] != 0     # 找到B列不为0
>index3 = (data['C'] != 0) & (data['D'] != 0)    # 找到C列和D列同时不为0
>
>data = data[index1 & index2 & index3]
>
>print(data.head(12))
>
>'''
>      ID       A          B     C     D
>0  54993  234188  580717.00   432  5234
>5  56972   76946  294585.00  2423   432
>7  22631  287230  276335.43    43    32
>8  32197   87401  321489.00    41   234
>'''
>```

