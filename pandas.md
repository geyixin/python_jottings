# pandas

+ pandas基本数据结构：Series，DataFrame
+ Series，就是列，类似一维数组，每个Series都有唯一表头，用来表示不同的Series
+ DataFrame，类似二维表格，每一列都是是个Series
+ Index，是为了定位Series中的元素，类似SQL中的主键，可以是字母、中文等，不一定数字

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
即实现以“菜品名称”索引
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

+ cumsum，groupby
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