# statsmodels

+ 此包注重对数据的统计建模分析

```python3
from statsmodels.tsa.stattools import adfuller as adf
from numpy import random
s = adf(random.rand(100))
print(s)
'''
(-2.827564080935731, 0.054443028212771284, 10, 89, {'1%': -3.506057133647011, '5%': -2.8946066061911946, '10%': -2.5844100201994697}, 32.73716089146424)
'''
```