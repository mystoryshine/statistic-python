### python实现概率分布

```python
# 导入包
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
sns.set()
plt.rcParams['font.sans-serif'] = ['SimHei']  #用来正常显示中文标签
plt.rcParams['axes.unicode_minus'] = False  #用来正常显示负号
```

- #### 离散型分布

  - 二项分布

    二项分布为 $n$ 重伯努利分布，当 $n=10$ ，成功的概率 $p=0.4$ 时，分布律计算如下：

    ```python
    n = 10        
    p = 0.4
    success_count_list = list(range(n+1))
    pmf_list = np.array([stats.binom.pmf(x,n,p) for x in range(n+1)])
    pd.DataFrame(np.expand_dims(pmf_list,axis=0),index=['P'])
    ax = sns.barplot(x=success_count_list,y=pmf_list)
    ax.set(xlabel='成功次数', ylabel='概率')
    ```

    ![](https://i.loli.net/2019/12/01/zYqsanTZSOC2ckL.png)

  - 泊松分布

    ```python
    mu = 2  # 平均值：每天发生2次事故
    target_count_list = list(range(11))  # 求发生 0 到 10 次事故的概率
    
    pmf_list = np.array([stats.poisson.pmf(x,mu) for x in target_count_list])
    pd.DataFrame(np.expand_dims(pmf_list,axis=0),index=['P'])
    ax = sns.barplot(x=target_count_list,y=pmf_list)
    ax.set(xlabel='发生事故次数', ylabel='概率')
    ```

    ![](https://i.loli.net/2019/12/01/ThRGoz5E6snSXmc.png)


- #### 连续型分布

  -  正态分布

      ```python
      mu = 5   # 平均值
      sigma = 3 # 标准差
      
      target_range = np.arange(-10,20,0.1)
      prob_list = stats.norm.pdf(target_range,mu,sigma)
      ax = sns.lineplot(x=target_range,y=prob_list)
      ax.set(xlabel='随机变量', ylabel='概率');
      ```

      ![](https://i.loli.net/2019/12/01/lCjSupH4LgPUZwA.png)

