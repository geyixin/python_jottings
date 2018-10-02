# sklearn

+ 机器学习库（不含神经网络），提供包括数据处理、分类、回归、聚类、预测、模型分析，，，

```python3
from sklearn import datasets, svm
iris = datasets.load_iris()
print(iris.data.shape)

clf = svm.LinearSVC()  # 建立线性SVM分类器
clf.fit(iris.data, iris.target)    # 训练，对监督而言是 fit(X,y)，非监督而言：fit(X)
clf.predict([[5.0, 3.6, 1.3, 0.25]])    # 输入数据预测
score = clf.score   # 看训练得分，得分越高，fit越好
paras = clf.coef_   # 查看训练好模型的参数
print(score)
print('---------------')
print(paras)
```

