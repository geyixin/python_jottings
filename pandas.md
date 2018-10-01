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
print(d.head())
print(d.tail())
print('--------------')
'''
   a  b  c
0  1  2  3
1  4  5  6
'''
print(d.describe())		# 对d做简约分析，最大值，最小值，均值等等
p = pandas.read_excel('data.xlsx')
print(p.head(2))	# 打印表格的前两行

```

