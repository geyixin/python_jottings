# matplotlib

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