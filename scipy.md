# scipy

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