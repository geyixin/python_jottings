# work as MATLAB

+ 包括方程组的求解、画图

### 1.求解线性方程组

```python3
from scipy.optimize import fsolve
# 求解非线性方程组 2x1-x2**2-1=0, x1**2-x2-2=0
def f(x):
    x1 = x[0]
    x2 = x[1]
    return [2*x1 - x2**2 - 1, x1**2 - x2 - 2]
print(fsolve(f, [1,1]))		# [1.91963957 1.68501606]
print(fsolve(f, [2,0]))		# [1.91963957 1.68501606]
```

### 2.画图

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

