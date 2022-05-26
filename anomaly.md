# anomaly



## what is an Anomaly 

An anomaly is an observation that deviates considerably from some concept of normality

异常现象是一种观察结果，它与正常性的某些概念有很大的偏离。



![[公式]](https://www.zhihu.com/equation?tex=%5Cmathcal%7BX%7D+%5Csubseteq+%5Cmathbb%7BR%7D%5E%7BD%7D) 是任务或应用的数据集。![[公式]](https://www.zhihu.com/equation?tex=%5Cmathbb%7BP%7D%5E%7B%2B%7D) 是正常样本的概率分布。![[公式]](https://www.zhihu.com/equation?tex=p%5E%7B%2B%7D%28%5Cboldsymbol%7Bx%7D%29) 其概率密度函数。异常样本集 ![[公式]](https://www.zhihu.com/equation?tex=%5Cmathcal%7BA%7D) 定义如下：

![[公式]](https://www.zhihu.com/equation?tex=%5Cmathcal%7BA%7D%3D%5Cleft%5C%7B%5Cboldsymbol%7Bx%7D+%5Cin+%5Cmathcal%7BX%7D+%5Cmid+p%5E%7B%2B%7D%28%5Cboldsymbol%7Bx%7D%29+%5Cleq+%5Ctau%5Cright%5C%7D%2C+%5Cquad+%5Ctau+%5Cgeq+0)





其中，![[公式]](https://www.zhihu.com/equation?tex=%5Cboldsymbol%7Bx%7D) 是数据集中的一个样本，若它的概率密度小于阈值 ![[公式]](https://www.zhihu.com/equation?tex=%5Ctau) ，则它是异常样本。![[公式]](https://www.zhihu.com/equation?tex=%5Ctau) 是一个足够小的值。



## 